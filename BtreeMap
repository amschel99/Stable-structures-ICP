pub struct BTreeMap<K, V, M>
where
    K: Storable + Ord + Clone,
    V: Storable,
    M: Memory,
{
    // The address of the root node. If a root node doesn't exist, the address
    // is set to NULL.
    root_addr: Address,

    version: Version,

    // An allocator used for managing memory and allocating nodes.
    allocator: Allocator<M>,

    // The number of elements in the map.
    length: u64,

    // A marker to communicate to the Rust compiler that we own these types.
    _phantom: PhantomData<(K, V)>,
}
