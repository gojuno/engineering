# RxJava 2 Migration

## Proposed Plan

* Migrate independent semi-standalone services.
* Migrate UI components where possible using interop to communicate with required services.
* Migrate remaining services since consumers (UI components) will be ready for such changes at this point.
* Remove interop and RxJava 1-related dependencies.

## Tips and Tricks

* Read [the official documentation](https://github.com/ReactiveX/RxJava/wiki/What's-different-in-2.0)
  carefully, it contains answers to most of your questions.
* At this point RxJava 1 and RxJava 2 can be used side-by-side without any consequences.
  All fundamental thingies, such as Retrofit adapter and custom operators are already in place,
  but you may need to write your own.
* Refer to a package migrated first when in doubt.
  You may find it useful as a starting searching point.
* Do not forget to change (and run) unit tests, this can and will presume the correct behavior.
  If there is no test, prefer to write it first if possible and reasonable.
* RxJava 2 crashes on `null` emissions. Make sure you are not consuming such streams.
  The final goal is to replace `Observable<T?>` with either `Observable<Optional<T>>`
  or `Optional<T>` everywhere, no exceptions.
* Migration changes should be as isolated as possible. Change god-like services
  and friends, last. It is always better to migrate a single atomic thing and test it properly
  instead of changing basically everything.
* Create a tech task for each migration with description what to recheck. Your testing team is really good,
  but help them out to catch possible issues.

