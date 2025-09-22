---
layout: post
title: Aren - Digimon Lab 1
subtitle: Art of Data Digimon Dataset Project
author: Aren Haroutunian
---

### Code to answer the 3 prompts
```python
import csv 

# This fuction counts how many Digimon in the dataset match a specific column and value
def count_digimon(column, value):
    counter = 0
    for row in data:
        if row[column] == value:
            counter+=1
    return counter

with open("datasets/digimon.csv", "r") as f:
    data = csv.DictReader(f)
    data = list(data)

    digimon_list = []
    spd = []

    # Loop through each Digimon 
    for row in data:
        speed = row["Spd"]
        spd.append(float(speed))

        name = row["Digimon"]
        atk = float(row["Atk"])
        memory = float(row["Memory"])
        digimon_list.append((name, atk, memory))
    
    valid_teams = []

    # Check every possible combination of 3 Digimon
    for i in range(len(digimon_list)):
        for j in range(i+1, len(digimon_list)):
            for k in range(j+1, len(digimon_list)):
                team = [digimon_list[i], digimon_list[j], digimon_list[k]]

                # Calculates total memory and attack for team
                total_memory = 0
                total_atk = 0
                for name, atk, memory in team:
                    total_memory += memory
                    total_atk += atk

                # Only keep teams with ≤ 15 memory and ≥ 300 attack
                if(total_memory <= 15 and total_atk >= 300):
                    valid_teams.append(team)
                        
    # Prints the first of these valid teams
    first_team = valid_teams[0]
    print("")
    print("Your Team:")

    total_memory = 0
    total_atk = 0

    for name, atk, memory in first_team:
        print(name, "- Attack:", atk, " - Memory:", memory)
        total_memory += memory
        total_atk += atk

    print("Total Attack:", total_atk)
    print("Total Memory", total_memory)
    
    # Average speed of all Digimon
    average = sum(spd) / len(spd)
    print("")
    print("Average speed of all Digimon:", average)
    
    print(count_digimon("Attribute", "Fire"))
```