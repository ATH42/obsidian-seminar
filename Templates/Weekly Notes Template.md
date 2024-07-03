---
type: weekly
date: <% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(0, 'days').format("YYYY-MM-DD") %>
---
#  <% tp.file.title %> - Weekly Log

> **Previous Week::** [[<% tp.date.now("YYYY-[W]ww", -7, tp.file.title, "YYYY-[W]ww") %>]]
> **Next Week::**  [[<% tp.date.now("YYYY-[W]ww", +7, tp.file.title, "YYYY-[W]ww") %>]]
> **Parent::** [[<% tp.date.now("YYYY-MM", 0, tp.date.now("YYYY-MM-DD")) %>]], [[<% tp.date.now("YYYY") %>]]
> ---

days:: [[ <% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(0, 'days').format("YYYY-MM-DD") %>]], [[ <% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(1, 'days').format("YYYY-MM-DD") %>]], [[ <% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(2, 'days').format("YYYY-MM-DD") %>]], [[ <% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(3, 'days').format("YYYY-MM-DD") %>]], [[ <% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(4, 'days').format("YYYY-MM-DD") %>]], [[ <% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(5, 'days').format("YYYY-MM-DD") %>]], [[ <% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(6, 'days').format("YYYY-MM-DD") %>]]

## Pictures
### 2023-W51
 ![Monday|200](<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(0, 'days').format("YYYY-MM-DD") %>#<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(0, 'days').format("YYYY-MM-DD") %>)
 
 ![Tuesday|200](<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(1, 'days').format("YYYY-MM-DD") %>#<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(1, 'days').format("YYYY-MM-DD") %>)
 
 ![Wednesday|200](<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(2, 'days').format("YYYY-MM-DD") %>#<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(2, 'days').format("YYYY-MM-DD") %>)
 
 ![Thursday|200](<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(3, 'days').format("YYYY-MM-DD") %>#<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(3, 'days').format("YYYY-MM-DD") %>)
 
 ![Friday|200](<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(4, 'days').format("YYYY-MM-DD") %>#<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(4, 'days').format("YYYY-MM-DD") %>)
 
 ![Saturday|200](<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(5, 'days').format("YYYY-MM-DD") %>#<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(5, 'days').format("YYYY-MM-DD") %>)
 
 ![Sunday|200](<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(6, 'days').format("YYYY-MM-DD") %>#<% moment(tp.file.title, "YYYY-[W]ww").startOf('week').add(6, 'days').format("YYYY-MM-DD") %>)
---
> [! orbit]- Sleep and weight
> ```dataviewjs
> const pages = dv.pages('"Journal/Daily"');
> const currentPage = dv.current();
> const startDate = new DateTime(currentPage.date);
> const endDate = startDate.plus(Duration.fromMillis(518400000));
>
> const data = pages.map((p) => ({
> date: p.date,
> logWeight: p.log_weight,
> 
> }));
>
> const filteredData = data
>  .filter((entry) => typeof entry.logWeight !== "undefined")
>  .filter((entry) => {
>    const entryDate = new DateTime(entry.date);
>    return entryDate >= startDate && entryDate <= endDate;
>  });
>
> const weightValues = filteredData.map((entry) => entry.logWeight);
>
> function calculateAverage(arr) {
>	let sum = 0; 
>	for (let i = 0; i < arr.length; i++) { 
>		sum += arr[i]; 
>	} 
>	return sum / arr.length; 
> }
>
> const averageWeight = calculateAverage(weightValues); 
> const averageWeightArr = Array(filteredData.length).fill(averageWeight);
>
> console.log('avArr', weightValues)
>
> const keysToInclude = [
> 	"logWeight",
> 	"averageWeight",
> ];
>
> const proxyArr = keysToInclude.map((key) =>
>  key === "logWeight" ? weightValues.values : averageWeightArr,
> );
>
> const distinctColors = [
> 	"rgba(255, 255, 204, 0.7)", 
> 	"rgba(229, 204, 255, 0.7)",
> ];
>
> const chartDataActivities = {
>  type: "line",
>  data: {
> 		 labels: filteredData.map((entry) => {
> 	     const date = new DateTime(entry.date);
> 	     return date.toLocaleString(DateTime.DATE_SHORT);
> 		  }),
>   datasets: keysToInclude.map((key, index) => ({
>      label: key,
>      data: proxyArr[index],
>      backgroundColor: [distinctColors[index]],
>      borderColor: [distinctColors[index].replace("0.7", "1")],
> 	 borderWidth: 1,
> 	 })),
> },
> };
>
> window.renderChart(chartDataActivities, this.container);
>```
>
>
>```dataviewjs
> const pages = dv.pages('"Journal/Daily"');
> const currentPage = dv.current();
>
> const startDate = new DateTime(currentPage.date);
> const endDate = startDate.plus(Duration.fromMillis(518400000));
>
> const data = pages.map((p) => ({
>  date: p.date,
>  cycling: p.log_cycling,
>  meditation: p.log_meditation,
>  strength: p.log_strength,
>  stretching: p.log_stretching
> }));
>
> const filteredData = data
> .filter((entry) => typeof entry.cycling !== "undefined")
>  .filter((entry) => {
>   const entryDate = new DateTime(entry.date);
>    return entryDate >= startDate && entryDate <= endDate;
> });
>
> const keysToInclude = [
> 	 "cycling",
> 	 "strength",
> 	 "stretching",
> 	"meditation",
> ];
>
> const averageValues = [];
> for (const key of keysToInclude) {
> let sum = 0;
> let count = 0;
>  for (const entry of filteredData) {
>    if (typeof entry[key] !== "undefined") {
>     sum += entry[key];
>      count++;
>    }
> }
>  const average = count ? sum / count : 0; // Avoid division by zero
>  averageValues.push(average);
> }
> 
> const distinctColors = [
> 	 "rgba(255, 204, 204, 0.7)",
> 	 "rgba(255, 229, 204, 0.7)", 
> 	 "rgba(204, 255, 204, 0.7)",
> 	 "rgba(204, 229, 255, 0.7)", 
> 	 "rgba(255, 204, 255, 0.7)", 
> 	 "rgba(255, 255, 204, 0.7)", 
> 	 "rgba(229, 204, 255, 0.7)", 
> 	 "rgba(204, 255, 255, 0.7)",
> ];
>
> const chartDataActivities = {
>  type: "pie",
> 	data: {
> 	   labels: keysToInclude,
> 	   datasets: [
> 			{
> 		       data: averageValues,
> 		       backgroundColor: distinctColors,
> 		       borderColor: distinctColors.map(color => color.replace("0.7", "1")),
> 		       borderWidth: 1,
> 		     },
> 	   ],
> 	 },
> };
>
> window.renderChart(chartDataActivities, this.container);
>

```dataviewjs
const pages = dv.pages('"Journal/Daily"');
const currentPage = dv.current();

const startDate = new DateTime(currentPage.date);
const endDate = startDate.plus(Duration.fromMillis(518400000));

const data = pages.map((p) => ({
  date: p.date,
  logSleepHours: p.log_sleep_hours,
  logWakeTime: p.log_wake_time,
}));

const filteredData = data
  .filter((entry) => typeof entry.logSleepHours !== "undefined")
  .filter((entry) => {
    const entryDate = new DateTime(entry.date);
    return entryDate >= startDate && entryDate <= endDate;
  });


const keysToInclude = [
	"logSleepHours",
	"logWakeTime"
];

console.log("filteredData");

const proxyArr = keysToInclude.map((key) =>
  filteredData.map((entry) => entry[key]),
);
const flattenedValues = proxyArr.map((a) => a.values);

const distinctColors = [
	"rgba(204, 255, 204, 0.7)", 
	"rgba(204, 229, 255, 0.7)",
];

const chartDataActivities = {
  type: "bar",
  data: {
    labels: filteredData.map((entry) => {
      const date = new DateTime(entry.date);
      return date.toLocaleString(DateTime.DATE_SHORT);
    }),
    datasets: keysToInclude.map((key, index) => ({
      label: key,
      data: flattenedValues[index],
      backgroundColor: [distinctColors[index]],
      borderColor: [distinctColors[index].replace("0.7", "1")],
      borderWidth: 1,
    })),
  },
};

window.renderChart(chartDataActivities, this.container);
```
---
## Reviews
> [! sun]- Morning Reviews
> ```dataview
> TABLE log_morning_review
> WHERE log_morning_review
> AND date >= this.date 
>  AND date <= date(this.date + dur(6 days))
> SORT date asc

> [!bed]- Day Reviews
> ```dataview
> TABLE log_day_review
> WHERE log_day_review
> AND date >= this.date 
>  AND date <= date(this.date + dur(6 days))
> SORT date asc

> [!bird]- Songs of the Week
> ```dataview
> TABLE log_song
> WHERE log_song
> AND date >= this.date 
>  AND date <= date(this.date + dur(6 days))
> SORT date asc
---
> [! pie]- Averages per topic
> ```dataviewjs
> const pages = dv.pages('"Journal/Daily"');
> const currentPage = dv.current();
>
> const startDate = new DateTime(currentPage.date);
> const endDate = startDate.plus(Duration.fromMillis(518400000));
>
> const data = pages.map((p) => ({
> 	date: p.date,
> 	logSleepHours: p.log_sleep_hours,
> 	logWakeTime: p.log_wake_time,
> 	creative: p.Creative_time,
> 	distraction: p.Distraction_time,
> 	maintenance: p.Maintenance_time,
> 	development: p.Personal_development_time,
> 	relationship: p.Relationship_time,
> 	play: p.Play_time,
> 	wellness: p.Wellness_time,
> 	work: p.Work_time,
> }));
>
> const filteredData = data
> 	.filter((entry) => typeof entry.logSleepHours !== "undefined")
> 	.filter((entry) => {
> 		 const entryDate = new DateTime(entry.date);
>    return entryDate >= startDate && entryDate <= endDate;
> 	});
>
> const keysToInclude = [
> 	 "creative",
> 	 "distraction",
> 	 "maintenance",
> 	 "development",
> 	 "play",
> 	 "work",
> 	 "relationship",
> 	 "wellness"
> ];
>
> const averageValues = [];
> for (const key of keysToInclude) {
> 	let sum = 0;
> 	let count = 0;
> 	for (const entry of filteredData) {
> 		   if (typeof entry[key] !== "undefined") {
> 		   sum += entry[key];
> 		     count++;
> 		   }
> 	}
>  const average = count ? sum / count : 0; // Avoid division by zero
>  averageValues.push(average);
> }
> 
> const distinctColors = [
> 	"rgba(255, 204, 204, 0.7)", 
> 	"rgba(255, 229, 204, 0.7)", 
> 	"rgba(204, 255, 204, 0.7)", 
> 	"rgba(204, 229, 255, 0.7)", 
> 	"rgba(255, 204, 255, 0.7)", 
> 	"rgba(255, 255, 204, 0.7)", 
> 	"rgba(229, 204, 255, 0.7)", 
> 	"rgba(204, 255, 255, 0.7)",
> ];
>
> const chartDataActivities = {
>  type: "pie",
> data: {
>    labels: keysToInclude,
>    datasets: [
>      {
>        data: averageValues,
>        backgroundColor: distinctColors,
>        borderColor: distinctColors.map(color => color.replace("0.7", "1")),
>        borderWidth: 1,
>      },
>    ],
>  },
> };
>
> window.renderChart(chartDataActivities, this.container);


```dataviewjs
const pages = dv.pages('"Journal/Daily"');
const currentPage = dv.current();

const startDate = new DateTime(currentPage.date);
const endDate = startDate.plus(Duration.fromMillis(518400000));

const data = pages.map((p) => ({
  date: p.date,
  sleepRating: p.log_sleep_rating,
  eating: p.healthy_eating,
  dayRating: p.log_day_rating,
}));

const filteredData = data
  .filter((entry) => typeof entry.sleepRating !== "undefined")
  .filter((entry) => {
    const entryDate = new DateTime(entry.date);
    return entryDate >= startDate && entryDate <= endDate;
  });

const keysToInclude = [
	"sleepRating",
	"eating",
	"dayRating",
	"averageDayRating"
];


const proxyArr = keysToInclude.map((key) =>
  filteredData.map((entry) => entry[key]),
);
const flattenedValues = proxyArr.map((a) => a.values);

const distinctColors = [
	 "rgba(255, 229, 204, 0.7)", 
	 "rgba(204, 255, 204, 0.7)", 
	 "rgba(204, 229, 255, 0.7)", 
	 "rgba(255, 204, 255, 0.7)", 
	 "rgba(255, 255, 204, 0.7)", 
	 "rgba(229, 204, 255, 0.7)", 
	 "rgba(204, 255, 255, 0.7)",
];

const dayRatingValues = filteredData.map((entry) => entry.dayRating); 
	let dayRatingSum = 0; 
	for (let i = 0; i < dayRatingValues.length; i++) { 
		dayRatingSum += dayRatingValues[i]; 
	} 
const averageDayRating = dayRatingSum / dayRatingValues.length;
const averagedDayRating = Array(filteredData.length).fill(averageDayRating); flattenedValues.push(averagedDayRating);

const chartDataActivities = {
  type: "line",
  data: {
    labels: filteredData.map((entry) => {
      const date = new DateTime(entry.date);
      return date.toLocaleString(DateTime.DATE_SHORT);
    }),
    datasets: keysToInclude.map((key, index) => ({
      label: key,
      data: flattenedValues[index],
      backgroundColor: [distinctColors[index]],
      borderColor: [distinctColors[index].replace("0.7", "1")],
      borderWidth: 1,
    })),
  },
};

window.renderChart(chartDataActivities, this.container);
```

# log_week_rating:: `=round((sum(nonnull(this.days.log_day_rating))/7) + 1 - 1,2)`
# log_week_review:: #on/weeklyReview