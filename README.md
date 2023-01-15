# Lending iterator

My concept for what a lending iterator crate should look like. **Work in progress**.

Most `Iterator` methods can work as is on `LendingIterator`s, but some wouldn't make sense. Basically any method that needs to look at more than one element at once isn't possible.

Some `LendingIterator` methods *may* return something that can act as an `Iterator`. For example `cloned`, or `map`, when the function passed to it returns a value that isn't tied to the lifetime of its input. In these cases, my design choice was to conditionally implement IntoIterator for the adapter.

## methods that behave the same on `LendingIterator`s as they do on `Iterator`s

* advance_by
* all
* any
* by_ref
* chain
* cmp
* cmp_by
* cloned
* copied
* count
* cycle
* enumerate
* eq
* eq_by
* filter
* filter_map
* find
* find_map
* flat_map
* flatten
* fold
* for_each
* fuse
* ge
* gt
* inspect
* intersperse
* intersperse_with
* is_partitioned
* le
* lt
* map
* map_while
* ne
* nth
* partial_cmp
* partial_cmp_by
* position
* product
* scan
* size_hint
* skip
* skip_while
* step_by
* sum
* take
* take_while
* try_find
* try_fold
* try_for_each
* zip

## methods that don't make sense on `LendingIterator`s

* array_chunks
* collect
* collect_into
* is_sorted
* is_sorted_by
* is_sorted_by_key
* last
* max
* max_by
* max_by_key
* min
* min_by
* min_by_key
* next_chunk
* partition
* partition_in_place
* peekable
* reduce
* try_collect
* try_reduce
* unzip

## methods that can sometimes be used to convert a `LendingIterator` into an `Iterator`

* cloned
* copied
* filter_map
* flat_map
* map
* map_while
* scan

## methods I'm not sure about

* rev
* rposition
