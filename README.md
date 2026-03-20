# Assignment 1 — Simulated Annealing: Exam Timetable Scheduling
## Observation Report

**Student Name  :** Kosuru Yasaswini
**Student ID    :** 2310040023 
**Date Submitted:** 20/03/2026  

---

## How to Submit

1. Run each experiment following the instructions below
2. Fill in every answer box — do not leave placeholders
3. Make sure the `plots/` folder contains all required images
4. Commit this README and the `plots/` folder to your GitHub repo

---

## Before You Begin — Read the Code

Open `sa_timetable.py` and read through it. Then answer these questions.

**Q1. What does `count_clashes()` measure? What value means a perfect timetable?**

```
`count_clashes()` measures the total number of conflicts in the timetable, where a conflict occurs if a student has two or more exams scheduled in the same time slot. It checks each student’s exam list and counts how many times slots overlap. A value of 0 means a perfect timetable with no clashes.
```

**Q2. What does `generate_neighbor()` do? How is the new timetable different from the current one?**

```
`generate_neighbor()` creates a new timetable by randomly selecting one exam and assigning it to a different time slot. It copies the current timetable and only changes the slot of that single exam. So, the new timetable is almost the same as the current one, except for one small modification.
```

**Q3. In `run_sa()`, there is this line:**
```python
if delta < 0 or random.random() < math.exp(-delta / T):
```
**What does this line decide? Why does SA sometimes accept a worse solution?**

```
This line decides whether to accept the new (neighbour) timetable or not. If the new solution is better (delta < 0), it is always accepted; if it is worse, it may still be accepted based on a probability.

Simulated Annealing sometimes accepts worse solutions to escape local minima and explore more possible solutions. This helps in finding a better overall (global) solution instead of getting stuck early.
```

---

## Experiment 1 — Baseline Run

**Instructions:** Run the program without changing anything.
```bash
python sa_timetable.py
```

**Fill in this table:**

| Metric | Your result |
|--------|-------------|
| Number of iterations completed | 1379|
| Clashes at iteration 1 |12 |
| Final best clashes |3 |
| Did SA reach 0 clashes? (Yes / No) |No |

**Copy the printed timetable output here:**
```
<img width="1350" height="900" alt="experiment_1" src="https://github.com/user-attachments/assets/ef80b37e-88cc-4909-821e-30db0db8ae32" />

```

**Look at `plots/experiment_1.png` and describe what you see (2–3 sentences).**  
*Where does the biggest drop in clashes happen? Does the curve flatten out?*
```
The biggest drop in clashes happens in the early iterations, where the value quickly decreases from around 12 to 6. After that, the improvement becomes slower and more gradual. Yes, the curve eventually flattens out, showing that the algorithm is stabilizing and finding fewer improvements over time.
```

---

## Experiment 2 — Effect of Cooling Rate

**Instructions:** In `sa_timetable.py`, find the `# EXPERIMENT 2` block in `__main__`.  
Copy it three times and run with `cooling_rate` = **0.80**, **0.95**, and **0.995**.  
Save plots as `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`.

**Results table:**

| cooling_rate | Final clashes | Iterations completed | Reached 0 clashes? |
|-------------|---------------|----------------------|--------------------|
| 0.80        |     8         |          31          |         No         |
| 0.95        |     3         |         135          |         No         |
| 0.995       |     3         |        1379          |         No         |

**Compare the three plots. What do you notice about how fast vs slow cooling affects the result? (3–4 sentences)**  
*Hint: Fast cooling = temperature drops quickly. Does it have time to explore well?*
```
With a fast cooling rate (0.80), the temperature drops very quickly, so the algorithm stops exploring early and gets stuck with a higher number of clashes (8). For moderate cooling (0.95), it performs better, reducing clashes to 3 with a reasonable number of iterations. With slow cooling (0.995), the algorithm explores more thoroughly and takes more iterations, but achieves a similarly low clash value. Overall, slower cooling allows better exploration and leads to improved solutions, while faster cooling gives quicker but poorer results.
```

**Which cooling_rate gave the best result? Why do you think that is?**
```
The best result was achieved with cooling_rate = 0.95 and 0.995, both giving the lowest clashes (3). However, 0.995 is slightly better because it explores more thoroughly due to slower cooling. This allows the algorithm to search more possible solutions and avoid getting stuck in poor local minima.
```

---

## Summary

**Complete this table with your best result from each experiment:**

| Experiment | Key setting | Final clashes | Main finding in one sentence |
|------------|-------------|---------------|------------------------------|
| 1 — Baseline | cooling_rate = 0.995 | 3|Slow cooling gives better solutions by allowing more exploration.  |
| 2 — Cooling rate | cooling_rate = ___ |3 |Higher cooling rates perform better as they avoid getting stuck early and search more thoroughly. |

**In your own words — what is the most important thing you learned about Simulated Annealing from these experiments? (3–5 sentences)**
```
The most important thing I learned is that Simulated Annealing balances exploration and optimization using temperature. A higher temperature at the start allows the algorithm to explore many possible solutions, even accepting worse ones. As the temperature decreases slowly, it focuses more on improving the solution and reducing clashes. The cooling rate plays a crucial role, as slow cooling leads to better results while fast cooling can make the algorithm get stuck early. Overall, proper tuning of parameters is key to achieving good performance.
```

---

## Submission Checklist

- [YES ] Student name and ID filled in
- [YES ] Q1, Q2, Q3 answered
- [ YES] Experiment 1: table filled, timetable pasted, plot observation written
- [ YES] Experiment 2: results table filled (3 rows), observation and answer written
- [YES ] Summary table completed and reflection written
- [ YES] `plots/` contains: `experiment_1.png`, `experiment_2a.png`, `experiment_2b.png`, `experiment_2c.png`
