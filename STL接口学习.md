```
#include <unordered_map>
```

# std::[unordered_map](https://cplusplus.com/reference/unordered_map/unordered_map/)::count

returns `1` if an element with that key exists in the container, and zero otherwise.

```
  std::unordered_multimap<std::string,std::string> myumm;
```

```
  myumm.reserve(7);
```

multimap 里也有 rehash reserve

If *n* is greater than the current number of buckets in the container ([bucket_count](https://cplusplus.com/unordered_multimap::bucket_count)), a rehash is forced. The new [bucket count](https://cplusplus.com/unordered_multimap::bucket_count) can either be equal or greater than *n*.

rehash  会自己调用，随着数据的增多。

reserve
If *n* is greater than the current [bucket_count](https://cplusplus.com/unordered_multimap::bucket_count) multiplied by the [max_load_factor](https://cplusplus.com/unordered_multimap::max_load_factor), the container's [bucket_count](https://cplusplus.com/unordered_multimap::bucket_count) is increased and a [rehash](https://cplusplus.com/unordered_multimap::rehash) is forced.

If *n* is lower than that, the function may have no effect.