1.  Hibernate = JPA implementation. Code against JPA, Hibernate does the work.

2.  Entity states: NEW → MANAGED → DETACHED → REMOVED.
    Detached = changes silently lost unless merge() called.

3.  Persistence Context = L1 cache + identity map + change tracker.
    Per session, NOT thread-safe, never share across threads.

4.  Dirty checking = automatic UPDATE on managed entity changes.
    No need to call save() inside @Transactional. (Interview trap!)

5.  Lazy = load on access (default for collections).
    Eager = load immediately (default for @ManyToOne).
    Prefer LAZY everywhere, fetch explicitly when needed.

6.  N+1 = 1 query for parents + N queries for children.
    Fix: JOIN FETCH, @EntityGraph, or @BatchSize.

7.  LazyInitializationException = lazy access after session closed.
    Fix: fetch in transaction, use DTOs, disable open-in-view.

8.  @Transactional fails silently on: self-invocation, private methods,
    checked exceptions (no rollback by default).

9.  L2 cache = cross-session, needs explicit setup (EHCache/Redis).
    L1 is always on, L2 is off by default.

10. For bulk ops / complex reports → skip Hibernate, use JDBC/JOOQ.
    Keep transactions short. Always paginate. Always use projections for reads.
