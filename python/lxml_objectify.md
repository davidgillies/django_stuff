Importing

    from lxml import objectify

Simply

    xml_string = open('Fenland.xml', 'r').read()
    xml_object = objectify.fromstring(xml_string)
    
Now tags can be accessed

    xml_object.some_tag
    
Attributes can be accessed

    xml_object.attrib['some_attrib']
    
Loop through tags

    for item in xml_object.thing:
        # where thng is a tag name when there is multiple of that tag
        print item.attrib['etc']
        
Creating an element

    my_elt = objectify.Element('{http://www.mrc-epid.cam.ac.uk/schema/common/epi}var_value') # url is the namespace.
    my_elt.value = 'bla'
    
