## What it does
1. Takes weight and height and return rounded BMI to a one decimal place.
2. Takes a list of daily step counts and an optional default (e.g 8000 steps) and returns a summary of the week.
3. Estimates calories burned from walking using approximately 0.04 calories per step.
4. Takes a list of daily fasting protocols and returns a count of how many days used each protocol.

## Usage
```python
#PROJECT 
#Function 1 BMI Calculator 

import math
def calculate_bmi(weight_kg, height_m):
    bmi = weight_kg/(height_m**2)
    return round(bmi, 1)
def bmi_category(bmi):
    if bmi < 18.5:
        return "Underweight"
    elif bmi < 25:
        return "Normal weight"
    elif bmi < 30:
        return "Overweight"
    else:
        return "Obese"

weight = 84
height = 1.78

bmi = calculate_bmi(weight, height)
print(f" Weight: {weight} kg")
print(f" Height: {height} m")
print(f" BMI: {bmi}")
print(f" Status: {bmi_category(bmi)}")

#Goal Checker
def weekly_steps_summary(steps_list, goal = 8000):
    days_hit = len([s for s in steps_list if s >= goal])
    average = sum(steps_list)/len(steps_list)
    best = max(steps_list)
    worst = min(steps_list)
    return{
        "days_on_goal" : days_hit,
        "total_days" : len(steps_list),
        "average" : round(average),
        "best_day": best,
        "worst_day" : worst,
    }
weekly = [9200, 7500, 10500, 8800, 6900, 11000, 9600]
result = weekly_steps_summary(weekly)

print(f"Step Summary:")
print(f" Days on goal: {result['days_on_goal']}/{result['total_days']}")
print(f" Average : {result['average']} steps")
print(f" Best day : {result['best_day']} steps")
print(f" Worst day : {result['worst_day']} steps")

#Calories
import math
def estimate_calories(steps, calories_per_step = 0.04):
    calories = steps * calories_per_step
    return math.floor(calories)

weekly_steps = [9200, 7500, 10500, 8800, 6900, 11000, 9600]
daily_cals = [estimate_calories(s) for s in weekly_steps]
print("Estimated daily calories burned from walking:")
days = ["Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun"]
for days, cals in zip(days, daily_cals):
    print(f"{days} : {cals} kcal")

#Protocol
def protocol_summary(protocol_list):
    unique = list(set(protocol_list))
    summary = {}
    for p in unique:
        summary[p] = protocol_list.count(p)
        return summary

    protocols = ["OMAD", "2MAD", "OMAD", "Autophagy Marathon", "OMAD", "2MAD", "OMAD"]
    result = protocol_summary(protocols)
    print("Protocol breakdown")
    for protocol, days in result.item():
        print(f" {protocol} : {days} days(s)")

#Full Report
import math
from datetime import date

#---DATA---
client_name = "James"
weight_kg = 84
height_m = 1.78
weekly_steps = [9200, 7500, 10500, 8800, 6900, 11000, 9600]
protocols = ["OMAD", "2MAD", "OMAD", "Autophagy Marathon", "OMAD", "2MAD", "OMAD"]
set_goal = 8000

#---FUNCTIONS---
def calculate_bmi(w,h):
    return round(w/(h**2))

def bmi_category(bmi):
    if bmi < 18.5:
        return "Underweight"
    elif bmi < 25:
        return "Normal weight"
    elif bmi < 30:
        return "Overweight"
    else: return "Obese"

def weekly_step_summary(steps, goal = 8000):
    return{
        "days_on_goal": len([s for s in steps if s >= 8000]),
        "average": round(sum(steps)/len(steps)),
        "best": max(steps),
        "worst": min(steps)
    }
def estimate_calories(steps, rate = 0.04):
    return math.floor(steps*rate)
def protocol_summary(plist):
    return{p: plist.count(p) for p in set(plist)}

#REPORT
today = date.today(). strftime("%d %B %Y")
bmi = calculate_bmi(weight_kg, height_m)
steps_report = weekly_step_summary(weekly_steps, set_goal)
total_cals = sum(estimate_calories(s) for s in weekly_steps)
proto_report = protocol_summary(protocols)

print("=" * 42)
print(f" WEEKLY REPORT: {client_name.upper()}")
print(f" Date: {today}")
print("=" * 42)
print(f"\nBODY")
print(f" Weight: {weight_kg} kg")
print(f" Height: {height_m} m")
print(f" BMI: {bmi} (bmi_category.(bmi))")
print(f"\nSTEPS (Goal: {set_goal})")
print(f" Day on goal: {steps_report['days_on_goal']}/7" )
print(f" Average: {steps_report['average']} steps/day")
print(f" Best day: {steps_report['best']} steps")
print(f" Worst day: {steps_report['worst']} steps")
print(f" Cals burned: ~{total_cals} kcal")
print(f"\nPROTOCOL BREAKDOWN")
for p, d in proto_report.items():
    print(f"{p} : {d} days(s)")
print("\n" + "=" * 42)
```
##Output
==========================================
 WEEKLY REPORT: JAMES
 Date: 12 October 2026
==========================================

BODY
 Weight: 84 kg
 Height: 1.78 m
 BMI: 27 (bmi_category.(bmi))

STEPS (Goal: 8000)
 Day on goal: 5/7
 Average: 9071 steps/day
 Best day: 11000 steps
 Worst day: 6900 steps
 Cals burned: ~2540 kcal

PROTOCOL BREAKDOWN
OMAD : 4 days(s)
2MAD : 2 days(s)
Autophagy Marathon : 1 days(s)

==========================================
