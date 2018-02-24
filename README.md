# sjs-base-model

Base Model help normalize raw data into models

```javascript
const apiData = {
        make: 'Tesla',
        model: 'Model S',
        YeAr: 2014,
        feature: {
            abs: true,
            airbags: true
        },
        colors: [{id: 'red' name: 'Red'}, {id: 'white' name: 'White'}]
}
```
```javascript
const carModel = new CarModel(data);
```
This is how you should extend `BaseBodel`
```javascript
export class CarModel extends BaseModel {
    
    make = '';
    model = '';
    year = null;
    feature = FeatureModel;
    colors = [ColorModel];
    
    constructor(data = {}) {
        super();
        
        if (data) {
            this.update(data);
        }
    }
    
    update(data) {
        super.update(data);
        
        this.year = data.YeAr;
    }
    
}
```
Model Explained 
```javascript
export class CarModel extends BaseModel {
    
    // The class properties must match the data properties being passed in. Otherwise they will be ignored
    make = '';
    model = '';
    year = null;
    
    // If data passed in is an object then a FeatureModel will be created
    // else the property will be set to null
    feature = FeatureModel;
    
    // If the data passed is an array then it will create a ColorModel for each item
    // else the property will be set to an empty array
    colors = [ColorModel];
    
    constructor(data = {}) {
        super();
        
        if (data) {
            this.update(data);
        }
    }
    
    update(data) {
        super.update(data);
        
        // If the data doesn't match the property name
        // You can set the value(s) manually after the update super method has been called.
        this.year = data.YeAr;
    }
    
}


```
Example how to use the `update` method which will only change the property value(s) that were passed in
```javascript
carModel.update({year: 2015, feature: {abs: true}});
```

##TypeScript Usage
You will need to do `as any` when assigning the function model to the type of model so the compiler doesn't complain. Notice `FeatureModel as any;` and `[ColorModel as any];`
```typescript
export class CarModel extends BaseModel {
    
    make: string = '';
    model: string = '';
    year: number = null;
    
    feature: FeatureModel = FeatureModel as any;
    
    colors: ColorModel[] = [ColorModel as any];
    
    constructor(data: any = {}) {
        super();
    
        if (data) {
            this.update(data);
        }
    }
    
    update(data: any): void {
        super.update(data);
        
        this.year = data.YeAr;
    }
    
}
```
