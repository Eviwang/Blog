## Array

- chunk

  ~~~javascript
  const chunk = (arr, size) =>
    Array.from({ length: Math.ceil(arr.length / size) }, (v, i) =>
      arr.slice(i * size, i * size + size)
    );
  ~~~

  ~~~javascript
  // 我的版本
  function chunk(arr,len){	
      if(arr.length<=len)return arr.slice(0);
      return [arr.splice(0,len)].concat([fn(arr,len)]);
  }
  ~~~

- all

  ~~~javascript
  const all = (arr,fn = Boolean) => arr.every(fn);		
  ~~~

- allEqual

  ~~~javascript
  const allEqual = (arr) => arr.every(x=>x === arr[0])
  ~~~

- any

  ~~~javascript
  const any = (arr, fn = Boolean) => arr.some(x=>fn(x))
  ~~~

- arrayToCSV

### 2019-9-17

- bifurcate

  ~~~javascript
  const bifurcate = (arr,filter)=>{
     return [arr.filter((x,i)=>filter[i]),arr.filter((x,i)=>!filter[i])]
  }
  ~~~

- bifurcateBy

- compact 移除false值

- countBy

- countOccurrences

- deepFlatten