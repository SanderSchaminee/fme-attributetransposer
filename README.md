# FME AttributeTransposer
Custom transformer for FME® that transposes attributes so that the value of a selected _Column Attribute_ is turned into a new attribute. In other words, this a simple version of the [AttributePivoter](https://www.safe.com/transformers/attribute-pivoter/), that flips the "rows" and "columns" of a feature attribute table.  

## Examples  
The table below shows the original input features and their attributes.  
When we set "Attribute2" as the _Column Attribute_ and the _Row Attributes_ to "Attribute4", "Attribute3" and "Attribute1" (in that order), we would end up with the 3 features, as shown in the second table.   

![Example Tables](https://github.com/SanderSchaminee/fme-attributetransposer/raw/master/example.png)  

The third table above shows what happens, when we set "Attribute3" as the _Column Attribute_ and the _Row Attributes_ to "Attribute1", "Attribute2", "Attribute4" and "Attribute5" (in that order). Notice that we have 4 features now and that the value "test" existed twice, which resulted in a "test" attribute and a "test(1)" attribute. The _Column Attribute_ also contains 2 empty values, that have been turned into "Untitled" and "Untitled(1)" respectively. This is intended behaviour: attributes cannot be overwritten or not written at all because their name is null, empty or missing.  
  
## Notes  
- The _AttributeTransposer_ creates attributes for _every_ feature that passes through it. Therefore, please use this transformer with great care.  
- The transformer will not preserve geometry. It only works on tabular data.  
- New attributes are created dynamically and should be exposed using an [AttributeExposer](https://www.safe.com/transformers/attribute-exposer/), for example.  
- All original attributes will still be exposed on the output feature, but will not have a value, except for the _Columns Attribute_. This attribute will store all the row attributes (i.e. "row headers") in the order that the user has selected.  
- Also available on [FME Hub](https://hub.safe.com/transformers/attributetransposer) for convenient installation.
- This transformer has been tested on Python 2.7 and 3.4.  
- If you notice a bug or desire a new feature, please [contact me](8972335+SanderSchaminee@users.noreply.github.com) or make a pull request!  
- Released under [GNU General Public License v3.0](https://github.com/SanderSchaminee/fme-attributetransposer/blob/master/LICENSE).  
- The [test workspace](https://github.com/SanderSchaminee/fme-attributetransposer/blob/master/AttributeTransposerTest.fmw) is used for testing and provides some examples.  

## Transformer Parameters  
### Columns Attribute    
Specify the attribute for which all feature values should be turned into new attributes (i.e. columns). The order in which features arrive, determines the order in which new attributes/columns are created, but since these attributes are not sequenced, this can't be guaranteed.

### Row Attribute(s)  
Select at least 1 attribute whose values will be used in a "row feature", effectively forming the attribute values of the _Columns Attribute_ set above. This means that the order in which you specify the _Row Attribute(s)_, determines the feature output order.