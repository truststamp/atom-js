OVERVIEW
========

Atom.js is a small, easy to use JavaScript class that provides asynchronous
control flow, event/property listeners, barriers, and more.


FEATURES
========

 - Under 9K (under 3K minified).
 - Works in a browser or in node.
 - No dependencies (except for running unit tests)


UNIT TESTS
==========

> node atom-test.js      // brief
> node atom-test.js -v   // verbose


EXAMPLES
========

	// Instanciate an atom.
	var a = atom.create();

	// Set some arbitrary properties on the atom.
	a.set({
		color: 'fugilin',
		spin: 1/3,
		module: 'My Module'
	});

	// Register listeners to be called...

	// ...whenever the property 'error' changes value.
	a.on('error', funtion (error) {
		console.log('There was a grevious calamity of code in ' + a.get('module'));
		console.log(error);
	});

	// ...only once, and only when the named properties have been initially set.
	a.once(['data_access', 'api_auth', 'doc_ready'], function (dal, api, doc) {
		api.selectColorTheme(a.get('color'));
		api.showUI(doc);
		a.set('initialized');
	});

	// ...only once, on the next change to the 'driving_coords' property.
	a.next('driving_coords', function (coords) {
		console.log('Are we there yet?');
	});

	// String together a series of asynchronous functions.
	a.chain(
		function (nextLink) {
			callAjaxMethod('foo', function (fooResult) {
				nextLink(fooResult);
			});
		},
		function (nextLink, fooResult) {
			callAjaxMethod('bar', function (barResult) {
				nextLink();
			});
		}
	);