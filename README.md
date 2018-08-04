# XlfParser
XML Localization Interchange File Format


[NuGet](https://www.google.com)
```c#
class Program
    {
        static void Main(string[] args)
        {
            XlfToClass();
            ClassToXlf();
        }

        static void XlfToClass()
        {
            string xml =
                "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<xliff version=\"1.2\" xmlns=\"urn:oasis:names:tc:xliff:document:1.2\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:schemaLocation=\"urn:oasis:names:tc:xliff:document:1.2 xliff-core-1.2-transitional.xsd\">" +
                    "<file datatype=\"xml\" source-language=\"en-US\" target-language=\"fr\" tool-id=\"UIStrings\">" +
                        "<header>" +
                            "<tool tool-id=\"Name\" tool-name=\"Name\" tool-company=\"TWyTec\"/>" +
                        "</header>" +
                        "<body>" +
                            "<group datatype=\"resx\">" +
                                "<trans-unit xmlns=\"\" id=\"Hi\">" +
                                    "<source>Hello World</source>" +
                                    "<target>Bonjour le monde</target>" +
                                    "<note>Hello World</note>" +
                                "</trans-unit>" +
                            "</group>" +
                        "</body>" +
                    "</file>" +
                "</xliff>";

            string xmlWithoutGroup =
                "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<xliff version=\"1.2\" xmlns=\"urn:oasis:names:tc:xliff:document:1.2\" xmlns:xsi=\"http://www.w3.org/2001/XMLSchema-instance\" xsi:schemaLocation=\"urn:oasis:names:tc:xliff:document:1.2 xliff-core-1.2-transitional.xsd\">" +
                    "<file datatype=\"xml\" source-language=\"en-US\" target-language=\"fr\" tool-id=\"UIStrings\">" +
                        "<header>" +
                            "<tool tool-id=\"Name\" tool-name=\"Name\" tool-company=\"TWyTec\"/>" +
                        "</header>" +
                        "<body>" +
                            "<trans-unit xmlns=\"\" id=\"Hi\">" +
                                    "<source>Hello World</source>" +
                                    "<target>Bonjour le monde</target>" +
                                    "<note>Hello World</note>" +
                                "</trans-unit>" +
                        "</body>" +
                    "</file>" +
                "</xliff>";

            var model = XlfParser.Converter.Deserialize(xml);
            var modelWithoutGroup = XlfParser.Converter.Deserialize(xmlWithoutGroup);
        }

        static void ClassToXlf()
        {
            XlfParser.Model.Xliff xliff = new XlfParser.Model.Xliff() {
                Version = 1.2m,
                File = new XlfParser.Model.File() {
                    Datatype = "xml",
                    SourceLanguage = "en-US",
                    TargetLanguage = "fr-fr",
                    ToolId = "Xlf",
                    Header = new XlfParser.Model.Header() {
                        Tool = new XlfParser.Model.Tool()
                        {
                            Id = "Xlf",
                            Company = "TWyTec",
                            Name = "Xlf"
                        }
                    },
                    Body = new XlfParser.Model.Body() {
                        TransUnit = new System.Collections.Generic.List<XlfParser.Model.TransUnit>()
                        {
                            new XlfParser.Model.TransUnit() { Id = "Hi", Note = "Hello World", Source = "Hello World", Target = "Bonjour le monde"}
                        }
                    }
                }
            };

            var xml = XlfParser.Converter.Serialize(xliff);
        }
    }
```

## License
MIT
