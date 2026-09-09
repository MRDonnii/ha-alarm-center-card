# HA Alarm Center Card

Et samlet alarm- og fejlcenter til Home Assistant. Kortet viser aktive alarmer fra konfigurerbare regler og kan midlertidigt skjule en alarm i 12 timer, til næste dag eller i syv dage.

## Funktioner

- Entity- og regexbaserede alarmregler
- Betingelser med `and` eller `or`
- Prioritering og tydelig aktiv/normal status
- Tidsbegrænset skjulning med fælles Home Assistant-lagring
- Mulighed for at vise en skjult alarm igen før tid
- Tema-farver med sikre fallback-værdier
- Responsivt design til desktop og mobil

## Installation

Tilføj repositoryet som et brugerdefineret HACS frontend-repository, eller placér filen i `/config/www/ha-alarm-center-card` og tilføj denne resource:

```yaml
url: /local/ha-alarm-center-card/ha-alarm-center-card.js
type: module
```

Opret en `input_text`-helper til de delte udløbstider:

```yaml
input_text:
  dashboard_alarm_snooze:
    name: Skjulte dashboardalarmer
    max: 255
```

## Eksempel

```yaml
type: custom:ha-alarm-center-card
title: Alarmer & fejl
snooze_entity: input_text.dashboard_alarm_snooze
alerts:
  - name: Hoveddøren er ulåst
    entity: lock.front_door
    operator: "="
    state: unlocked
    priority: 3
    icon: mdi:lock-alert
```

Alarmregler understøtter `=`, `!=`, `<`, `<=`, `>` og `>=`. Brug `entity_filter` i stedet for `entity` for at matche flere entities med et regulært udtryk. Valg gemmes som `entity_id@udløbstid`, så den skjulte status følger brugeren på tværs af enheder.

## Licens

MIT
