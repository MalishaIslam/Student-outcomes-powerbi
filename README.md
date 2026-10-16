# Student Outcomes Dashboard (Power BI)

Built by **Malisha Islam Tapotee** · [Portfolio](https://malishaislam.github.io/)

An interactive two-page Power BI dashboard analysing about 32,600 course-enrollment records from the
[Open University Learning Analytics Dataset (OULAD)](https://archive.ics.uci.edu/dataset/349/open+university+learning+analytics+dataset).
It shows how students finish their courses (pass, distinction, fail or withdraw) and how those outcomes
vary by course module, semester, education level and region.

This is the analytics companion to my [Student Success Tracker](https://github.com/MalishaIslam/student-success-tracker),
a SQL Server + ASP.NET Core web app built on the same dataset.

**Tools:** Power BI Desktop · Power Query · DAX

## Screenshots

| Overview | Outcome Analysis |
| --- | --- |
| ![Overview page](images/overview.png) | ![Outcome Analysis page](images/outcome-analysis.png) |

A static copy of the full report is in [`Student-Outcomes-Dashboard.pdf`](Student-Outcomes-Dashboard.pdf).

## Report pages

| Page | What it shows |
| --- | --- |
| **Overview** | KPI cards (total enrollments, pass rate, withdrawal rate, distinction rate), students by region, and slicers for course module, gender and age band |
| **Outcome Analysis** | Outcomes by course module, pass rate by education level, pass-rate trend across semesters, and the overall outcome distribution |

Page-navigation buttons move between the two pages, and the slicers are synced so a filter chosen on
the Overview page also applies to the Outcome Analysis page.

## How it was built

1. **Data preparation (Power Query):** loaded `studentInfo.csv`, checked and set column data types.
2. **DAX measures:**

   ```DAX
   Total Students   = COUNTROWS(studentInfo)
   Pass Rate        = DIVIDE(CALCULATE([Total Students], studentInfo[final_result] IN {"Pass","Distinction"}), [Total Students])
   Withdrawal Rate  = DIVIDE(CALCULATE([Total Students], studentInfo[final_result] = "Withdrawn"), [Total Students])
   Distinction Rate = DIVIDE(CALCULATE([Total Students], studentInfo[final_result] = "Distinction"), [Total Students])
   ```

   Pass Rate counts both *Pass* and *Distinction* as successful completions.
3. **Visuals:** cards, donut chart, stacked bar chart, clustered column chart, line chart and treemap,
   with custom titles and formatting.
4. **Interactivity:** synced slicers, cross-filtering between visuals, and page navigation buttons.

## Key findings

- **Fewer than half of enrollments end in a pass.** 47.2% pass (including 9.3% with distinction),
  21.6% fail and 31.2% withdraw.
- **Prior education matters.** Students with a postgraduate qualification pass about 65% of the time,
  compared with about 30% for students with no formal qualifications.
- **Autumn-start runs do better.** Course runs starting in October (the "J" runs) have higher pass rates
  than those starting in February (the "B" runs) in both 2013 and 2014.
- **Modules differ in size and outcome mix.** BBB and FFF are the largest modules, and some modules
  (for example CCC) lose a much larger share of students to withdrawal.

## Open the report

Download `Student-Outcomes-Dashboard.pbix` and open it in
[Power BI Desktop](https://www.microsoft.com/power-platform/products/power-bi/desktop) (free, Windows).
The data is already imported into the file.

## Data and licence

Kuzilek, J., Hlosta, M. & Zdrahal, Z. (2017). *Open University Learning Analytics dataset.*
Scientific Data 4, 170171. <https://doi.org/10.1038/sdata.2017.171>. Licensed
[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). The dataset is anonymised.
