# SDN - Simple Data Notation
The simplest, most extensible serialization format I can think of. I may be wrong about some of the details, but I think the underlying idea is solid. Please open an issue if you would like to correct me on naming or attributes of the data structures I define, or if you feel that anything here is unclear.

### Purpose
This format is to be used in a similar way as JSON or EDN, however it is designed to avoid the language-specific idiosyncracies that JSON and EDN have inherited from their parent languages. JSON can represent arrays and dictionaries (called "objects" in Javascript). If one would like to represent a set in JSON, this would need to be shoehorned into an array and later decoded by some arbitrary parser in application code. EDN uses a lot of very Clojure-specific syntax, and has a focus on the data structures available in that language. SDN, on the other hand, is designed to be as neutral as possible.

## Primitives
SDN consists of a few primitives:
- **Brackets:** These are two characters, and opening and closing bracket. There is only one variety of bracket in EDN. I'm going to go with the square bracket for now `[]`, because I feel they are the prettiest, but I am open to any suggestions.
- **Structure tag:** This is a sequence of characters that follows an opening bracket and specifies what type of data structure follows. Indicating data structure types with a tag rather than some different type of bracket is what gives SDN its extensibility. For example: `[arr` indicates that the characters up until the next `]` are part of an array.
- **Item delimiter:** `,` seperates items in a data structure. This is just the same as JSON. The last item in a data structure can optionally be followed by a `,`, even if this imparts no useful information. For example, this is an array: `[arr 1, 2, 45]`
- **Key-value delimiter:** `:` seperates keys and values in data structures that incorporate them. This is also the same as JSON. For example, here is a dictionary (known as an 'object' in JSON): `[dict "foo": "bar", "bonanza": "heyo"]`
- **String:** A string. This gets put into double quotes `"string"`. I have not worked out the details around encoding etc. yet. Open an issue if you have suggestions.
- **Number:** A number is written without quotes. Any unquoted sequence of alphanumeric characters that is not a structure tag can be considered a number. I'm not at all sure about what type or precision of number should be used, and very open to suggestions. Please open an issue about this.

NOTE: Whitespace is ignored by EDN.

## Data structures
With the primitives defined above, we can begin to build data structures. I'm going to start with the structures available in Javascript ES6, as this is the language I am most familiar with.

`//TODO`
