##  其他技巧

`rmdir 目录 /Q /S` 删文件会比较快



## 指令

- *ngFor="let item of items"
- *ngIf
- (click)="add(item)"  ()括号用来事件绑定, 事件需要调用。
- [href] 属性绑定
- {{}} 插值





## 组件

`@Input()` 装饰器指出其属性值是从该组件的父组件商品列表组件中传入

```javascript
export class ProductAlertsComponent implements OnInit {
  @Input() product;
  constructor() { }

  ngOnInit() {
  }

}
```



输出：

```javascript
 @Input() product;
 @Output() notify = new EventEmitter();
<p *ngIf="product.price > 700">
  <button (click)="notify.emit()">Notify Me</button>
</p>
```

```javascript
<app-product-alerts
  [product]="product" 
  (notify)="onNotify()">
</app-product-alerts>
```





## 参考 

- [文档](<https://angular.cn/guide/architecture>)