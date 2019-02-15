# View Plan Component and Add to Plan

> Some text here from fiona

Lets create a view-plan component

```bash
ng g c activities/view-plan
```

In the activities.service.ts file create a new public method getPlan\(\) which returns our list of activities.

**...\daily-planner\src\app\services\activities.service.ts**

```typescript
public getPlan(){
  return this.dailySchedule;
}
```

Inject the activities service into view-plan.component.ts by adding it to the constructor

**...\daily-planner\src\app\activities\view-plan\view-plan.component.ts**

```typescript
import { ActivityModel } from 'src/app/data/activity.model';
import { ActivitiesService } from 'src/app/services/activities.service';
```

```typescript
constructor(private activitesService: ActivitiesService) { }
```

Declare a variable planList of type ActivityModel array inside the opening brackets of the export class

```typescript
planList: ActivityModel[];
```

In ngOnInit\(\) call the function getPlan\(\) and assign it to planList variable.

```typescript
  ngOnInit() {
    this.planList = this.activitesService.getPlan();
  }
```

In the view-plan.component.html file add

**...\daily-planner\src\app\activities\view-plan\view-plan.component.html** 

```markup
<div id="daily-schedule">
  <h1>Schedule a plan</h1>
  <div *ngIf="planList.length <= 0">
    The daily schedule is currently empty
  </div>
  <div class="daily-schedule-list" *ngFor="let item of planList">
    <div class="daily-schedule-item">
      <h2>{{ item.name }}</h2>
      <i class="fas {{ item.image }} circle-icon"></i>
      <button class="btn-remove">
        ×
      </button>
    </div>
  </div>
    <button id="btn-share" class="screen-only">Print</button>
  <button id="btn-reset" class="screen-only">
    Reset
  </button>
</div>
```

Add the app-view-plan selector to activities.component.html above the existing code

**...\daily-planner\src\app\activities\activities.component.html**

```markup
<app-view-plan></app-view-plan>
```

