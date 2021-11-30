# ~ DocGen: The Document Generator ~
> Generate documents quickly using Python templates and JSON data.

_Created by [Nathan Foottit](https://github.com/nat-foo) and [Tom Holownia](https://github.com/TomHolownia). Originally written for [Aether](https://survansix.itch.io/aether-edit)._

This document generator was written to generate and modify the API for a game engine. It reads JSON files in `/input`, parsing the data through Python templates in `/templates`. This allows the quick creation and revision of vast quantities of customised content.

## How to Use

_For an example use-case, feel free to run the docgen.py out of the box._

### 1. Create a JSON file with the following format:
* Entries with #'s in front and behind are for you to put in yourself.
* The `_default` entry at the beginning is optional, if you would like a default template.
* The `_filename` entry is what the new file created will be called.
* The `_templates` entry connects Python templates to the JSON data.
* The `...`'s indicate that you can add as many more entries here as you require.
* [#template1#, #template2#, ...] etc. refers to the specific python templates you would like. The order of these gives the order that they will appear in the file.
* #optional_property1# etc. gives optional properties that you can use in the code. For example, if you wanted a `type` entry that was unique to each file, you would put this here. The #value# of this entry can be in the format of a dictionary, list, or string.

JSON structure:

    {
        "_default":[#template1#, #template2#, ...]
        "#firstfilename#":{
            "_filename": #filename#
            "_templates": [#template1#, #template2#, ...]
            #optional_property1#: #value#
            #optiona2_property1#: #value#
            ...
        }
        "#secondfilename#":{
            "_filename": #filename#
            "_templates": [#template1#, #template2#, ...]
            #optional_property1#: #value#
            #optiona2_property1#: #value#
            ...
        }
        "#thirdfilename#":{
                "_filename": #filename#
                "_templates": [#template1#, #template2#, ...]
                #optional_property1#: #value#
                #optiona2_property1#: #value#
                ...
        }
        ...
    }

### 2. Create a python file returning a string.

You can create this string in whichever way pleases you, but it is highly recommended to make use of Python's `f-string` templates which have the following form:

    f"""Here is some text.
    Here `{{class_name}}` would write the value of `class_name` to the string.
    """

Using loops and appropriate information flow will allow you to create a string in such a way as to 
represent even larger quantities of code.

Providing that the Python file is in the `templates` folder, and that  file returns a string, a file will be generated by DocGen.

### 3. Link the Python Template and the JSON is done by the following steps:

1. Write and place a Python script (.py) in the `templates` folder
2. Write a JSON file that has the template included in either the `_default` or `_templates` property. Extra properties added will be read by DocGen, and can be used in the Python Templates.
3. Run DocGen.

Once this process is complete, if you need to add to or amend your code, you can simply change the template or JSON file. This will allow you to make, say, a small (or large!) change to every file in your document at the press of a button.
