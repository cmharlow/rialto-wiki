The current use cases for Rialto point us toward a need for some kind of graph- or triple-based datastore. Vitro is this, and MUCH more. Adding a dependency on an entire application framework instead of adding a dependency on a data store is problematic because:

* It requires developers to gain knowledge not just on the datastore itself, but also the larger Vitro ecosystem, and how the (TDB) datastore interacts with it.
* When a new release of Vitro comes out, we'll have more work to do in order to update it since the install is far from trivial (using a container could alleviate this to some degree, although the container definition still has to be written and maintained). If we use a standalone datastore, the update will be simpler.
* Setting up a development environment and keeping it standardized across laptops becomes more complicated (although again using a container could alleviate this to some degree).
* There may be potential conflicts if we wish to update TDB or other components to a later version than what Vitro supports (unless we take ownership of Vitro ourselves).
* Using Vitro makes it harder to switch to a different datastore later.
* Vitro requires us to run Tomcat, which is problematic with the out-of-the-box TDB datastore (see https://github.com/sul-dlss/rialto/wiki/Comparing-triplestores).