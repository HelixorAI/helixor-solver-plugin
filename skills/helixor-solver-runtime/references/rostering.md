# Rostering example

Rostering uses the same explicitly configured `solver` and answer contract as
routing, but needs the full solver dependency set and the applicable embedded
entitlement or service authority. See the
[Preview deployment tutorial](https://helixor.dev/tutorials/solver-deployment-models.html)
and [version record](contracts.md#versions-and-sources).

After configuring `solver` with either tested deployment model, this supplied
example asks for two non-overlapping eight-hour shifts and gives two qualified
employees eight hours each:

```python
roster_problem = {
    "employees": [
        {"id": "e1", "skills": ["rn"], "max_hours": 8},
        {"id": "e2", "skills": ["rn"], "max_hours": 8},
    ],
    "shifts": [
        {"id": "s1", "day": 0, "start_hour": 8, "duration": 8,
         "required_staff": 1, "required_skills": ["rn"]},
        {"id": "s2", "day": 1, "start_hour": 8, "duration": 8,
         "required_staff": 1, "required_skills": ["rn"]},
    ],
}
roster_answer = solver.solve("rostering", roster_problem)
assert roster_answer["verdict"] == "feasible", roster_answer["shortfalls"]
assert roster_answer["solution"] is not None
print(roster_answer["metadata"]["model"], roster_answer["verdict"])
```

Keep the actual engine/certificate rather than expecting one particular
assignment ordering. Removing either employee leaves eight available hours for
sixteen required hours: pre-solve advice reports the deficit, and the checked
solve returns `infeasible` with `solution=None` and ranked alternatives.
It must not label an undercovered or over-hours roster as the original solution.

Real workforce models need the supplied skill/eligibility, overlap, rest,
hours, coverage and preference rules mapped to their actual constraints.
The small example does not establish those additional business requirements.
Do not copy a routing engine option into a roster call; inspect the installed
roster contract and report the engine that actually ran.
