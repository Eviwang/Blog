## autocomplted 有个selectionChange事件

```javascript

        <input
          nz-input
          formControlName="teamLeader"
          [nzAutocomplete]="auto"
          (input)="onInput($event.target?.value)"
          id="teamLeader"
        />
        <nz-autocomplete [nzBackfill]="true" (selectionChange)="selectOption($event.nzValue)" #auto>
          <nz-auto-option *ngFor="let option of teamLeaderList" [nzValue]="option.name">
            {{ option.name }}
          </nz-auto-option>
        </nz-autocomplete>
```





**不一定要用autocomplted的，可以使用 select**



## 自带响应式断点

```javascript


// 注入：public breakpointObserver: BreakpointObserver；

breakpointObserver.observe([Breakpoints.Large, Breakpoints.Medium, Breakpoints.Small]).subscribe(x => {
      console.log(x);
      if (x.breakpoints[Breakpoints.Small]) {
        this.breakpoint = 2;
      } else if (x.breakpoints[Breakpoints.Medium]) {
        this.breakpoint = 4;
      } else if (x.breakpoints[Breakpoints.Large]) {
        this.breakpoint = 8;
      }
    });
```



## 父传子组件

```javascript
currentEditTeam = new Subject();

传给子组件时：
team.subscribe(x=>{});
```

