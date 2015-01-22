# SDN - Simple Data Notation
The simplest, most extensible serialization format I can think of. I may be wrong about some of the details, but I think the underlying idea is solid. Please open an issue if you would like to correct me on naming or attributes of the data structures I define, or if you feel that anything here is unclear.

### Purpose
This format is to be used in a similar way as JSON or EDN, however it is designed to avoid the language-specific idiosyncracies that JSON and EDN have inherited from their parent languages. Instead of indicating different data structures with different types of brackets, the type of data structure is indicated with a tag immediately preceding it. This makes it possible to represent an unlimited number of data structures with a very simple format.

```
// JSON
{
  "hash": "w32fwfw33",
  "message": {
    "timestamp": "29304857",
    "content": {
      "name": "richard",
      "scores": [4, 5, 3, 6]
    }
  }
}

// SDN
dict[
  "hash": "w32fwfw33",
  "message": dict[
    "timestamp": 29304857,
    "content": dict[
      "name": "richard",
      "scores": arr[4, 5, 3, 6]
    ]
  ]
]
```

## Primitives
SDN consists of a few primitives:
- **Brackets:** These are two characters, and opening and closing bracket. There is only one variety of bracket in EDN. I'm going to go with the square bracket for now `[]`, because I feel they are the prettiest, but I am open to any suggestions.
- **Structure tag:** This is a sequence of characters that precedes an opening bracket and specifies what type of data structure follows. Indicating data structure types with a tag rather than some different type of bracket is what gives SDN its extensibility. For example: `arr[` indicates that the characters up until the next `]` are part of an array.
- **Item delimiter:** `,` seperates items in a data structure. This is just the same as JSON. The last item in a data structure can optionally be followed by a `,`, even if this imparts no useful information. For example, this is an array: `arr[1, 2, 45]`
- **Key-value delimiter:** `:` seperates keys and values in data structures that incorporate them. This is also the same as JSON. For example, here is a dictionary (known as an 'object' in JSON): `dict["foo": "bar", "bonanza": "heyo"]`
- **String:** A string. This gets put into double quotes `"string"`. I have not worked out the details around encoding etc. yet. Open an issue if you have suggestions.
- **Number:** A number is written without quotes. Any unquoted sequence of alphanumeric characters that is not a structure tag can be considered a number. I'm not at all sure about what type or precision of number should be used, and very open to suggestions. Please open an issue about this.

NOTE: Whitespace is ignored by SDN.

## Data structures
With the primitives defined above, we can begin to build data structures. I'm going to start with the structures available in Javascript ES6, as this is the language I am most familiar with.

### Array
This is a data structure consisting of an in-order set of values. There is no requirement for the items to be unique, or to all be of the same type. Values can be other data structures.

`arr[1, "foo", 34, "foo"]`

### Dictionary
This is a data structure consisting of an out-of-order set of key value pairs. Keys must be strings. Values can be any value or data structures.

`dict["foo": "bar", "damn": 34]`

### Set
This is a list of unique items in-order. A non-unique item is a syntax error.

`set[1, "foo", 34]`

### Map
This is like the dictionary, except the keys can be any value or data structure.

`map[arr[1, 2]: "bar", "damn": 34]`
