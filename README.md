# sequence-rpg
### generates professional random sequences
---
![alt text](https://img.shields.io/github/package-json/v/turbokirichenko/sequence-rpg?style=for-the-badge)
![alt text](https://img.shields.io/github/repo-size/turbokirichenko/sequence-rpg?style=for-the-badge)
---
## Getting Started
```
$ npm i sequence-rpg --save-dev

```
## NodeJS
```js
const generator = require('sequence-rpg');
```

## Simple example
```js
const generator = require('sequence-rpg');

const sequences = new generator({ minNumber: 1, maxNumber: 10 }) // config object

const result = sequences.make({ // schema as object
	level: Number // type for key: "level"
}, 3); // size of sequence

console.log(result);

// *console*
//
// [
//	{ level: 2 },
//	{ level: 1 },
//	{ level: 5 }
// ]
//
```

## Commonly example
```js
// create array from object
const result = sequences.make({ 
	name: "SuperMan123", //constant value
	age: { 				 //custom type
		type: Number,    	//type
		max: 99, 	 	 	//opts
		min: 18  		 	//opts
	},
	friends: [{ 		 //random array
		name: String, 		//type
		age: {				//custom type
			type: Number,
			max: 99,
			min: 18,
		}
	}]
}, 2); 

console.log(result);

// *console*
//
// [
//	{
//	 name: 'SuperMan123',
//	 age: 23,
//	 friends: [
//		{
//			name: <random String>,
//			age: 87
//		},
//		{
//			name: <random String>,
//			age: 55
//		}
//	 ]
//  },
//  {
//   name: "SuperMan123",
//   ...
//  }
//]
```

## Extremely example
```js
//your custom type:
const MyCustomType = (opts) => { //opts param required!!!
	const race = opts.race(); //getter!!!
	const name = opts.name();
	return `name: ${name}, race: ${race}`;
}

//special Linker type
const Linker = sequences.Linker;

//special RandomValueFromList type
const List = sequences.RandomValueFromList;

const result = sequences.make({ 
	unit: {
		id: String,
		race: List("Orc", "Elf", "Human", "Dwarf", "Unicorn"),
	},
	info: {
		type: MyCustomType,
		name: "Admin",
		race: Linker("unit.race") //copy value from <obj>.unit.race
	},
	copy: Linker("info.race") //return undefined, because info.race is option property
}, 2); 


// *console*
//
// [
//	{
//	 unit: { id: "122f1ac271279127ffa", race: 'Human' },
//	 info: 'name: Admin, race: Human',
//   copy: undefined
//	},
//  {
//	 unit: { id: "47628facd21de12a189", race: 'Orc' },
//	 info: 'name: Admin, race: Orc',
//   copy: undefined
//	}
//]
```
---

## More Example 

* [docs](https://github.com/turbokirichenko/sequence-rpg/blob/main/index.test.js)
* [issues](https://github.com/turbokirichenko/sequence-rpg/issues)
* [open code](https://github.com/turbokirichenko/sequence-rpg)
