# transit_assistant





## Initial Shortcut Outline:

 1. Find Calendar Events
Action: Find Calendar Events
Filters:
Start Date: Today
Limit: 10 events
Sort by: Start Date

2. Repeat with Each Item
Action: Repeat with Each
Items: Calendar Events (from the previous action)
Inside the loop:
Set Variable: Current Event = Repeat Item
Set Variable: Next Event = Repeat Item + 1

3. Get Event Details
Action: Get Event Details
Event: Current Event (variable from the repeat loop)
Details:
Start Date
End Date
Location
Action: Get Event Details
Event: Next Event (variable from the repeat loop)
Details:
Start Date
Location

4. Calculate Duration (Time Gap)
Action: Calculate Duration Between Dates
Start Date: End Date of Current Event
End Date: Start Date of Next Event
Result: Store as Time Gap (in minutes)

5. Get Weather Forecast
Action: Get Weather Forecast
Location: Location of Current Event
At: End Time of Current Event
Details: Hourly forecast
Action: Get Details of Weather
Weather Condition: Rain Chance
Store in Variable: RainChance (as percentage)

6. Get Travel Time (Walking)
Action: Get Travel Time
Start: Location of Current Event
End: Location of Next Event
Mode: Walking

7. Get Travel Time (Public Transit)
Action: Get Travel Time
Start: Location of Current Event
End: Location of Next Event
Mode: Public Transit

8. Get Travel Time (Driving)
Action: Get Travel Time
Start: Location of Current Event
End: Location of Next Event
Mode: Driving

9. If/Otherwise (Rain Check)
Action: If
Condition: RainChance > 50%
Actions If True:
Set Variable: WalkingAvailable = False (no walking if it’s raining)

10. If/Otherwise (Walking Decision)
Action: If
Condition: Walking Time < 15 minutes and RainChance < 50%
Actions If True:
Set Variable: Preferred Mode = Walking

11. If/Otherwise (Public Transit Check)
Action: If
Condition: Public Transit Time > 90 minutes or Public Transit Time > Time Gap
Actions If True:
Set Variable: Preferred Mode = Driving

12. Set Variable (Final Mode)
Action: Set Variable
Variable: Final Mode = Preferred Mode (based on the decisions above)

13. Text (Formatted Output)
Action: Text
Text Content:

14. Show Result
Action: Show Result
Display: Output from the Text action (above)
Event [Start] - [End] → [Title]  
📍 [Location]  
☁️ Rain: [RainChance]%  
🕒 Travel Time Options:  
  🚶 Walking: [Walking Time] mins  
  🚌 Public Transit: [Transit Time] mins  
  🚗 Driving: [Driving Time] mins  
✅ Recommended Mode: [Final Mode]
