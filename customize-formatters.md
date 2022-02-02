# How to customize formatters

Formatters in Geonetwork are different ways to visualize a record of metadata.

Take [this record](https://antarcticdatacenter.cnr.it/geonetwork/srv/eng/catalog.search#/metadata/77b344c6-1d10-11eb-bccd-7b40b3c96977) as example. You can view it with:

- an **HTML** formatter:
  
  https://antarcticdatacenter.cnr.it/geonetwork/srv/api/records/77b344c6-1d10-11eb-bccd-7b40b3c96977

- a **XML** formatter:
  
  https://antarcticdatacenter.cnr.it/geonetwork/srv/api/records/77b344c6-1d10-11eb-bccd-7b40b3c96977/formatters/xml

- a **jsonLd** formatter:
  
  https://antarcticdatacenter.cnr.it/geonetwork/srv/api/records/77b344c6-1d10-11eb-bccd-7b40b3c96977/formatters/jsonld

and many others.

What if we want to customize a formatter? We can do so.

Formatters are defined in the Geonetwork `data` directory. How we can find where this directory is? We can look in the admin console under **Admin Console > Statistics and status > Information**. In my case the folder is located at `/var/lib/geonetwork_data`.

Every metadata standard in Geonetwork has his formatters. Suppose we want to customize the **jsonLd** formatter of the **iso19139** standard.

The file to modify is:

`/var/lib/geonetwork_data/config/schema_plugins/iso19139/formatter/jsonld/iso19139-to-jsonld.xsl`

Inside the file we have the jsonLd keys and values. In this example I added a `citation` key with the value taken from `Identification Info > Code` metadata record field. The value is extracted with the XPath to his position in the iso19139 schema definition.

```xml
"citation": <xsl:apply-templates mode="toJsonLDLocalized"
                                 select="gmd:identificationInfo/*/gmd:citation/*/gmd:identifier/*/gmd:code"/>
```
Save the file and restart Geonetwork.



