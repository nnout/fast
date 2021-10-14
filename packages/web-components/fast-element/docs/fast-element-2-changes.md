# Changes in FASTElement 2.0

## Breaking Changes

* `HTMLDirective` - The `targetIndex: number` property has been replaced by a `targetId: string` property. The `createBehavior` method no longer takes a target `Node` but instead takes a `BehaviorTargets` instance. The actual target can be looked up on the `BehaviorTargets` instance by indexing with the `targetId` property.
* `compileTemplate()` - Internals have been significantly changed. The implementation no longer uses a TreeWalker. The return type has change to an `HTMLTemplateCompilationResult` with different properties.
* `View` and `HTMLView` - Type parameters added to enable strongly typed views based on their data source. The constructor of `HTMLView` has a new signature based on changes to the compiler's output. Internals have been cleaned up and no longer rely on the Range type.
* `ElementViewTemplate`, `SyntheticViewTemplate`, and `ViewTemplate` - Added type parameters throughout. Logic to instantiate and apply behaviors moved out of the template and into the view where it can be lazily executed.
* `DOM` - Tree Walker methods are no longer used and are thus removed. The API for removing child nodes has been removed as well since it was only used in one place and could be inlined.
* `class` - Bindings to `class` are now more nuanced. Binding directly to `class` will simply set the `className` property. If you need to bind to `class` knowing that manual JS will also manipulate the `classList` in addition to the binding, then you should now bind to `:classList` instead. This allows for performance optimizations in the simple, most common case.