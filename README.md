# rust-geo-normalized

Creates a new instance of the rust geo/geo-types Polygon/Multipolygon that follows the OGC winding rules. 

The rust geo and geo-types crates are not as strict as the OGC guidelines, and allow for polygons with inner and outer rings in any winding order. This trait returns a Polygon/Multipolygon where all outer rings are clockwise, and all inner rings are anti-clockwise.

## Examples

```rust
// Anti-clockwise winding order for outer ring
let bad = polygon![
        (x: 1.0, y: 1.0),
        (x: 4.0, y: 1.0),
        (x: 4.0, y: 4.0),
        (x: 1.0, y: 4.0),
        (x: 1.0, y: 1.0),
        ];

// Clockwise winding order for outer ring
let good = polygon![
        (x: 1.0, y: 1.0),
        (x: 1.0, y: 4.0),
        (x: 4.0, y: 4.0),
        (x: 4.0, y: 1.0),
        (x: 1.0, y: 1.0),
        ];

let norm = bad.normalized();
// norm should have the same points and shape as `bad` but in the valid winding order
assert_eq!(norm, good);
```