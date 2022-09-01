const并未区分出编译期常量和[运行期](https://www.zhihu.com/search?q=运行期&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra={"sourceType"%3A"answer"%2C"sourceId"%3A63798713})常量

constexpr限定在了编译期常量

为了能在编译过程中随时展开，constexpr函数被隐式地指定为内联函数。

inline 函数在编译阶段就展开的函数，以消除运行时产生额外的开销。