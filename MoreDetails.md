# More Details

Here are some details that have been identified.

## Advantages

- It is safe to use pyexiv2.Image.read_*(). These methods does not affect the image in any way. (md5 unchanged)
- If you try to access a non-standard key, an exception will be raised.

    ```python
    >>> i = Image(r"pyexiv2/tests/1.jpg")
    >>> i.modify_exif({"Exif.Image.myflag001": "test"})       # Unallowed
    RuntimeError: (Caught Exiv2 exception) Invalid tag name or ifdId `myflag001', ifdId 1
    ```

## Defects

- Not thread-safe, because some global variables are used.
- Some special metadata couldn't be converted to string type, making it uneditable.
- If the metadata contains "\v\f", it will be replaced with "\v\b".
- if the XMP metadata contains '\v' or '\f', it will be replaced with space ' '.