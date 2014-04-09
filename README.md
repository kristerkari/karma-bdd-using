karma-bdd-using
===============

DRY your Karma + Jasmine or Mocha tests using the data provider pattern

A test helper for Jasmine and Mocha frameworks, inspired by this article: [DRYing Up Your JavaScript Jasmine Tests With the Data Provider Pattern](http://blog.jphpsf.com/2012/08/30/drying-up-your-javascript-jasmine-tests)

## Installation

```sh
npm install karma-bdd-using
```

and add `'bdd-using'` to your Karma config frameworks:

```js
frameworks: ['jasmine', 'bdd-using'],
```

## Examples

Sometimes you need to write a test where all tested values are expected to have the same test result:

```js
describe("when calling isLeap method", function() {

	it("should return true for leap years", function() {
		expect(isLeap(1976)).to.equal(true);
		expect(isLeap(1980)).to.equal(true);
		expect(isLeap(1984)).to.equal(true);
		expect(isLeap(1988)).to.equal(true);
		expect(isLeap(1992)).to.equal(true);
		expect(isLeap(1996)).to.equal(true);
	});

	it("should return false for non-leap years", function() {
		expect(isLeap(1975)).to.equal(false);
		expect(isLeap(1981)).to.equal(false);
		expect(isLeap(1985)).to.equal(false);
		expect(isLeap(1989)).to.equal(false);
		expect(isLeap(1993)).to.equal(false);
		expect(isLeap(1997)).to.equal(false);
	});	

});

```

With `using` helper you can write this instead:

```js
describe("when calling isLeap method", function() {

	using("leap years", [1976, 1980, 1984, 1988, 1992, 1996], function(year) {
		it("should return true", function() {
			expect(isLeap(year)).to.equal(true);
		});
	});

	using("non-leap years", [1975, 1981, 1985, 1989, 1993, 1997], function(year) {
		it("should return false", function() {
			expect(isLeap(year)).to.equal(false);
		});
	});

});
```

And get a nicer test output:

```
  when calling isLeap method
    ✓ should return true (with "leap years" using "1976") 
    ✓ should return true (with "leap years" using "1980") 
    ✓ should return true (with "leap years" using "1984") 
    ✓ should return true (with "leap years" using "1988") 
    ✓ should return true (with "leap years" using "1992") 
    ✓ should return true (with "leap years" using "1996") 
    ✓ should return false (with "non-leap years" using "1975") 
    ✓ should return false (with "non-leap years" using "1981") 
    ✓ should return false (with "non-leap years" using "1985") 
    ✓ should return false (with "non-leap years" using "1989") 
    ✓ should return false (with "non-leap years" using "1993") 
    ✓ should return false (with "non-leap years" using "1997")
```    
