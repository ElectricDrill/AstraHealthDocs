# Lifesteal

Lifesteal is a mechanic that lets an entity recover health proportional to the damage it deals. When an entity successfully damages a target, a percentage of the damage — determined by a configurable stat — is healed back to the attacker.

The system supports **two lifesteal layers**:

1. **Generic Lifesteal** — configured once in `AstraRpgHealthConfigSO` and applied to all damage dealt by the entity.
2. **Damage-Type Lifesteal** — configured directly inside each `DamageTypeSO` and applied only when that specific damage type is dealt.

Both layers use the same `LifestealStatConfig` structure, so designers configure the same three concepts in both places: the lifesteal stat, the heal source, and the damage amount selector. If both layers are configured for the same hit, their heal amounts stack. Depending on the `Unify Lifesteal Heals` flag in `AstraRpgHealthConfigSO`, those stacked amounts can be applied either as two separate heals or as a single unified heal.

## LifestealStatConfig

`LifestealStatConfig` is the reusable data structure used by both **Generic Lifesteal** and the per-`DamageTypeSO` **Lifesteal** section.

**Lifesteal Stat**  
The stat that drives the lifesteal percentage. At runtime, the attacker reads this stat value from its own `StatSet` and computes the heal as:
> heal amount = basis damage × (lifesteal stat value / 100)

The stat value is read as a `Percentage` type, meaning the raw `long` value stored in the stat is divided by 100 internally. A stat value of `15` therefore corresponds to 15% lifesteal. For lifesteal to activate, this stat must be present in the dealing entity's `StatSet`.

**Lifesteal Source**  
The `HealSourceSO` used when applying the lifesteal heal. As with any heal in the framework, the heal source determines which heal modifiers — flat and percentage — are applied to the resulting heal, so lifesteal heals can be boosted or reduced by modifiers associated with the configured `HealSourceSO`. See [Heal Source](healing.md#heal-source) for details on `HealSourceSO` configuration.

**Amount Selector**  
Determines which damage value is used as the basis for the lifesteal computation. See [Amount Selector](#amount-selector) below.

## Generic Lifesteal

`AstraRpgHealthConfigSO` exposes a **Generic Lifesteal** field of type `LifestealStatConfig`.

If its **Lifesteal Stat** is configured and the damage dealer has that stat in its `StatSet`, every successful hit can generate lifesteal from this generic configuration regardless of the hit's `DamageTypeSO`.

Use this when you want a broad mechanic such as "all outgoing damage grants lifesteal", without repeating the same setup on every damage type.

See also: [Lifesteal](package-configuration.md#lifesteal) in Package Configuration.

## Damage-Type Lifesteal

Each `DamageTypeSO` contains its own **Lifesteal** field, also of type `LifestealStatConfig`.

This contribution is evaluated only when the resolved hit uses that `DamageTypeSO`. It stacks with **Generic Lifesteal**, making it possible to define a baseline lifesteal that applies to all damage plus an additional bonus or alternate source for specific damage types.

Use this when lifesteal should depend on the nature of the damage — for example, only physical hits lifesteal, or fire damage lifesteal should use a dedicated `HealSourceSO`.

See also: [Damage Type's Lifesteal](damage.md#damage-types-lifesteal).

### Amount Selector

The Amount Selector controls which damage value is sampled as the lifesteal basis. Three modes are available:

- **Final** *(default)*: uses the damage value after all pipeline steps — the damage actually applied to the target. This is the most intuitive mode for a straightforward "heal for a percentage of damage dealt" mechanic.
- **Initial**: uses the raw damage value before any pipeline modifications. Useful when you want lifesteal to reflect the attacker's power output regardless of the target's defenses — for example, a vampire's lifesteal that scales with their attack power rather than with how much the target's armor reduced.
- **Step**: samples the damage value at a specific pipeline step. You select a step and whether to use the value recorded before (`Pre`) or after (`Post`) that step executes, giving designers precise control over which phase of the calculation drives the heal. Refer to [Damage Calculation Pipeline](damage.md#damage-calculation-pipeline) for an overview of the available pipeline steps.

The following image shows the inspector when Step mode is selected:  
![Amount Selector - Step mode](../../images/AstraRPG/workflows/lifesteal/amount-selector-step.png)

> [!NOTE]
> If **Step** mode is selected but no step is configured, the system falls back to **Final** damage. The inspector displays a warning to indicate this condition.

## Separate vs Unified Heals

When both **Generic Lifesteal** and **Damage-Type Lifesteal** contribute to the same hit, the framework can apply them in two different ways. By default, `Unify Lifesteal Heals` is enabled, so the two contributions are merged into a single heal.

### Separate Heals

When `Unify Lifesteal Heals` is **disabled**, each contribution produces its own heal:

- the generic contribution uses the generic `Lifesteal Source`
- the damage-type contribution uses the damage type's `Lifesteal Source`

This is the right choice when those two heal sources should remain distinguishable for heal modifiers, event listeners, combat logs, analytics, or VFX/UI feedback.

### Unified Heal

When `Unify Lifesteal Heals` is **enabled** *(default)*, the generic and damage-type lifesteal amounts are summed and applied as a **single heal**.

In this mode, the `HealSourceSO` is resolved as follows:

- use the damage type's `Lifesteal Source` if the damage-type contribution is active and that source is configured
- otherwise fall back to the generic `Lifesteal Source`

This is useful when generic lifesteal is meant to be an invisible baseline bonus and you want the final heal to behave as a single gameplay event.

## Performance Considerations

> [!NOTE]
> Before making any considerations about performance, keep in mind that premature optimization is the root of all evil. A real performance problem should be identified through profiling before taking any action.

By default, lifesteal heals raise the standard healing events (`Pre Heal` and `Entity Healed`). In games where many entities deal lifesteal damage frequently — for example, a horde of enemies all with a lifesteal stat, each landing hits several times per second — the volume of heal events generated can become significant, especially when the global `Entity Healed Event` has multiple listeners.

If profiling reveals this to be a bottleneck, the **Suppress Lifesteal Events** flag in `AstraRpgHealthConfigSO` disables healing event emission for lifesteal heals entirely. The heal is still applied; only the events are suppressed. This option is appropriate when you do not need to react to lifesteal heals through event listeners — for example, when your UI or combat log does not track lifesteal healing specifically.

A similar consideration applies to passive health regeneration, which can also generate a high volume of heal events under certain conditions. See [Performance Considerations](healing.md#performance-considerations) in the Healing documentation for a broader discussion.

## Conditions

> [!NOTE]
> Lifesteal is evaluated after every damage application. The following conditions must all be met for it to trigger:
> - The dealing entity is the source of the damage. Lifesteal does not trigger on damage dealt by others.
> - The dealing entity is alive at the moment of damage resolution.
> - At least one lifesteal layer is configured for the hit:
>   - **Generic Lifesteal** in `AstraRpgHealthConfigSO`, and/or
>   - **Lifesteal** on the hit's `DamageTypeSO`.
> - For each configured layer, the corresponding **Lifesteal Stat** is present in the dealing entity's `StatSet`.
> - The computed heal amount for that layer is greater than zero. A lifesteal stat of 0% produces no heal contribution.

> [!IMPORTANT]
> Lifesteal relies on the **Global Damage Resolution Event** being correctly configured on each entity's `EntityHealth`. This event is used by the framework to propagate damage outcomes across all listening entities — including the attacker, which uses it to detect its own successful hits and trigger lifesteal. Assigning a non-global event to this slot will break lifesteal and other framework features that depend on centralized damage communication. See [Global Events](entity-health.md#global-events) for setup details.
