#### vsi::runtime::Buffer
This utility class provides method to store and retrieve binary data.

#### Function Reference
- `Buffer()`: Construct an empty buffer.
- `Buffer(size_t len)`: Construct a buffer.
	- `len`: Size of the buffer to construct.
- `Buffer(const char *string)`: Construct a buffer using a null terminated string. The length and content are same as string's.
	- `string`: The input string.
- `Buffer(void *_data, size_t len, bool direct = false)`: Construct a buffer using a data pointer and given length.
	- `_data`: Pointer of the data to copy from.
	- `len`: Size of the buffer to construct.
	- `direct`: If this parameter is true then buffer will not allocate nor copy the content but use the provided pointer as the preallocated memory.
- `put(const unsigned char _byte, int _offset)`: Copy a single byte into the buffer at the given offset.
	- `_byte`: Byte to copy into the buffer.
	- `_offset`: This will be used as the target offset into the buffer for the copy operation.
- `put(Buffer *src, int _offset = 0)`: Copies another `Buffer`'s contents into this buffer at the given offset.
	- `src`: Pointer to the source buffer.
	- `_offset`: This will be used as the target offset into the buffer for the copy operation.
- `getInt()`: Returns an integer value and forwards the current offset by it's size.
	return: The integer value stored at current offset.
- `compare(Buffer &buf)`: Compares the content of this buffer with another Buffer.
	- `buf`: Pointer to another `Buffer` to compare against.
	- return: true if the contents are identical. False otherwise.
- `putInt(int i)`: Stores an integer at the current offset and forwards the offset by integer's size.
	- `i`: Integer value to store in the buffer.
- `fill(const char *pattern)`: Fills the buffer with the given pattern. The pattern is repeated to fill the whole buffer. If the pattern is bigger than the buffer then only the portion that it is clipped.
	- `pattern`: A pattern to fill in the buffer. A null terminated string is required.
- `getShort()`: Return a short value at current offset and forward the offset by short size.
	- return: The short value that is at current offset.
- `putShort(short i)`: Write the short value at current offset and forward the offset by short size.
	- `i`: Short value to write.
- `getChar()`: Read a char value at current offset and forward the offset by char size.
	- return: The char value that is at current offset.
- `putChar(char i)`: Write the char value at current offset and forward the offset by char size.
	- `i`: Char value to write.
- `size()`: Returns the size of the buffer minus current offset. Note that internal size might be larger than the value return if offset is > 0;
	- return: Readable size of the buffer (size - offset).
- `get()`: Returns the underlying raw pointer of stored data at current offset.
	- return: Pointer to the data.
- `rewind()`: Rewinds the buffer, setting the offset at zero.
- `data()`: Returns the underlying raw pointer of stored data at current offset.
- `base_size()`: returns the total size of the underlying buffer. Note that this is the overall memory size that is used by the buffer, not affected by the current offset.
	- return: total size of the underlying buffer.
- `base_data()`: Returns the raw pointer of the underlying buffer. The pointer is to the base and is not affected by current offset.
	- return: raw pointer to the underlying buffer.
- `substr(size_t size)`: Returns a part of buffer clipped to the specified size.
	- `size`: Only return these many bytes.
	- return: std::string containing the clipped buffer. If buffer size was larger than passed size, it is appended by `...` to indicate clipping status.
- `bytes(size_t size, const char *separator)`: Returns a string formatted as hexadecimal and separated by the provided separator character.
	- `size`: limit the return string to this size.
	- `separator`: user this character as the separator.
	- return: std::string formated as hexadecimal string.
- `offset()`: Returns the current offset of the buffer.
	- return: integer specifying the current offset.
- `set(const void *_data, size_t len)`: Sets the buffer contents. The underlying buffer will resize to accommodate the new size.
	- `_data`: Pointer to raw content to copy.
	- `len`: Size of the content to copy. Also used as the new size for this buffer.
- `set(const char *string)`: Sets the buffer contents to a null terminated string. The underlying buffer will resize to accommodate the new size.
	- `string`: the null terminated string to use as the content and to calculate the new size of the buffer.
- `direct_set(void *_data, size_t _size)`: Change the buffer to use the provided raw buffer as the underlying buffer. The provided raw buffer should be allocated using malloc or new and will be freed by this `Buffer` when it's destructor is called.
	- `_data`: Pointer to the raw buffer.
	- `_size`: Size of the raw buffer;
- `add(const void *_data, size_t len)`: Appends data to the current buffer. The underlying buffer will be resized to accommodate the new size.
	- `_data`: Pointer to the data.
	- `_size`: Size of the raw buffer;
- `add(Buffer *buf)`: Appends another Buffer's contents to the current buffer. The underlying buffer will be resized to accommodate the new size.
	- `buf`: Pointer to the `Buffer` to copy the data from.
- `offset(size_t _offset)`: Sets the current offset to provided value.
	- `_offset`: New offset value. It should not be larger than the underlying buffer's size.
- `dev_offset(size_t _offset)`: An auxiliary piece of integer that is used to specify the target offset to write the data once it reaches it's destination.
	- `_offset`: Offset to write the data to. The offset is only enforced for memory devices.
- `dev_offset()`: Returns the memory offset where the buffer should be written to.
	- return: Returns the auxiliary offset.
- `reduce(size_t size)`: Truncates the buffer by provided size. The truncated bytes are permanently lost.
	- `size`: Truncate the underlying buffer by this size. The overall size of the buffer must be larger or equal to the provided size.
- `alloc(size_t len)`: Allocate the given size for the underlying buffer. If there was an existing buffer than it is freed.
	- `len`: The new size of the underlying buffer.
