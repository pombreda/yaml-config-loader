yaml-config-loader
==================

Takes care of loading configuration from yaml file and validating it using schema.

Example
-------

config.yml:


    required_string: abc
    section:
      subsection:
        required_int: 123

Custom loader class with defined schema:

    import ycl

    class MyConfig(ycl.Config):
    
        schema = {
            "required_string": ycl.StringEntry(required=True),
            "section": {
                "subsection": {
                    "required_int": ycl.IntegerEntry(required=True)
                },
                "optional_int": ycl.IntegerEntry(),
            }
        }

Load configuration using our class:

    cfg = MyConfig.from_file('config.yml')

    cfg.required_string
    >>> u'abc'
    
    cfg.section.subsection.required_int
    >>> 123
    
    cfg.dump()
    >>> {'required_string': u'abc', 'section': {'subsection': {'required_int': 123}}}

If any required option is missing from configuration file or if it's invalid ConfigurationError will be raised.
