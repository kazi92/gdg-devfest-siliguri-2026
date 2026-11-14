> Paste everything below the line into Google AI Studio, or use the notebook for the full hands-on version.

# Demo pack: "Building Leonida for Real"

Paste everything below the line into Google AI Studio (any current Gemini model), run it, and screenshot the response for slide 17 ("What comes back"). All data is synthetic.

---

You are a senior campus facilities engineer. A tech conference is running in the Main Hall today.

## 1. The map: telemetry (CSV)

```
time,ch2_chw_supply_c,ch2_cond_pump_flow_pct,ahu3_supply_air_c,hall_temp_c,hall_co2_ppm,hall_people
10:15,7.0,100,13.0,23.8,610,300
10:30,7.0,100,13.1,24.1,690,420
10:45,7.6,91,13.6,24.6,780,510
11:00,8.9,80,14.8,25.3,860,580
11:15,10.4,70,16.2,26.1,930,615
11:30,11.8,62,17.5,26.9,980,620
```

Equipment status at every reading: CH-2 = RUNNING, AHU-3 = RUNNING.

## 2. The relationships: campus graph

- Chiller CH-2 FEEDS Air handler AHU-3
- AHU-3 SERVES Main Hall
- DevFest event OCCUPIES Main Hall (sessions until 17:00; lunch break 13:00–14:00)
- Main Hall EXITS_VIA Gate 1 (main) and Gate 3 (side, usually closed)
- Chiller CH-1 is on STANDBY and can serve AHU-3

## 3. The world outside: Weather API forecast

- 12:00: 32 °C · 13:00: 34 °C · 15:00: 35 °C, sunny

## 4. The rules: SOP-FM-04 (excerpt)

- Chilled water supply: 6–8 °C
- Occupied hall temperature: 26 °C maximum
- CO₂ in occupied spaces: 1000 ppm maximum
- Starting or stopping a chiller needs approval from the facility head
- Gates and anything to do with fire or life safety are never changed automatically

## 5. The ask

Using the telemetry, the graph, the forecast and the SOP:

1. Find what's abnormal and which asset it started on.
2. Predict the Main Hall's conditions for the next hour.
3. Recommend specific actions.
4. Give each action an autonomy level from 1★ to 5★:
   1★ observe · 2★ recommend (human decides) · 3★ act after human approval · 4★ act then report · 5★ fully autonomous.
   Respect the SOP: chiller changes need approval, and nothing involving gates or life safety goes above 2★.

Keep the answer short and structured with the headings: Finding, Next hour, Actions.
