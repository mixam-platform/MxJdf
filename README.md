# Mixam Job Description Format
## API & SDK for ordering a print job

The Mixam Job Description Format is a definition of a structure describing a print job in an unambiguous way.

Although the Mixam platform is capable of describing a job in many formats (cXML, OneFlow and vendor specific formats), the MXJDF (Mixam Job Description Format)  is the most useful of them all and the recommended way to establish an automated connection with us.    

The format is made of attributes and values and can be implemented in XML and JSON syntax. We provide a Java implementation of the MXJDF format but it can easily be implemented by other programing languages such as PHP or JavaScript. 

Mixam offers the protocol as a JSON document or an XML document. 

The document can be attached to an email message or posted to the printer preferred end-point.

Table of content
The top level	3
Element: job	5
Element: article	6
Element: component	7
Element: chromaticity	8
Element: format	8
Element: material	9
Element: refining	10
Element: processing	11
Element: binding	13
Element: details	14
Element: shipment	14
Element: RecipientAddress	15
Element: address	16
Element: senderForLabel (Address)	16
Type: Address	17
Element: delivery	18
Element: File	20
Element: export	20
JSON Example	21
XML Example	23

# The top level
The top level of the MxJdf document contains the following elements:
```javascript
{
  "version": 3.08,
  "desc": "mixam.job.description",
  "dateCreated": 1579177108174,
  "author" : "Mary Ansell",
  "referencedJobNumber": 303171489,
  "price" : 105.31,
  “currencyCode”: “gbp”,
  "job": {...},
  "files": [...],
  "export": {...}
}
```
| Property  | Description | Values |
|---|---|---|
|version| Current version of the protocol. (String)  | Currently ‘3.08’|
|desc|Document description. (String)|Always "mixam.job.description"|
|dateCreated|Epoch date of creation. (Long number)|A Unix Timestamp of the date the document was created|
|author|The name of the person who created the document. (String)|   |
|referencedJobNumber|The associated order’s id in the Mixam system. (String)|   |
|price|The pre-agreed cost price of the job (Double precision number)|   |
|currencyCode|The currency in which the price is specified. (String)|“GBP”, “USD”, “CAD”, “AUD”|
|job|A map of properties describing the job.|See bellow|
|files|A list of artwork files associated with the job. (List<File>)|See bellow|
|export|A map of properties describing the export value of the goods. (Map). Applicable only when goods are shipped overseas.| See bellow.|

# Element: job
```javascript
"job": {
    "article": {...},
    "details": {...},
    "shipment": {...}
}
```
article
The article describes the print requirements (map)
See bellow
details
Contains some meta data regarding the number of copies, tax and alternative id. (map)
See bellow
shipment
Contains addresses and delivery details
See bellow


# Element: article
```javascript
"article": {
  "components": [...],
  "type": 0,
  "product": 1,
  "subProduct": 100001
 }
````
components
A list of components (such as text, cover, dust jacket etc.) (List<component>)
See bellow
type
Taxation type (VAT, GST etc.) (ArticleTaxType)
EXEMPT(0),
VAT(1),
GST(2),
USA_TAX(3);


product
The product id (ProductGroupType)
INVALID(0),
PRODUCT_BRUCHURES(1),
PRODUCT_FLYERS(2),
PRODUCT_FOLDED(3),
PRODUCT_POSTERS(4),   PRODUCT_LETTERHEADS(5),
PRODUCT_PHOTOBOOK(6),
PRODUCT_BOOK(7),  PRODUCT_BUSINESS_CARD(8),
PRODUCT_POSTCARD(9),  PRODUCT_GREETING_CARD(10)
PRODUCT_NOTEPAD(11),    PRODUCT_COMPLIMENT_SLIPS(12),    PRODUCT_ENVELOPES(13),
PRODUCT_FOLDERS(14),
PRODUCT_LAYFLAT(15),
PRODUCT_WALL_CALENDARS(16),    PRODUCT_DESK_CALENDARS(17),    PRODUCT_VR_WALL_CALENDARS(18) PRODUCT_VR_DESK_CALENDARS(19)  PRODUCT_TRADITIONAL_BOOK(20);


subProduct
Fine classification of the product. (optional) (SubProductType)
PRODUCT_HARD_COVER_BOOKS(100001)
PRODUCT_PAPERBACK_BOOKS(100002)
PRODUCT_PERFECT_BOOKLETS(100003)
PRODUCT_WIRO_BOOKLETS(100004)   PRODUCT_LOOP_BOOKLETS(100005)  PRODUCT_STAPLED_BOOKLETS(100006) PRODUCT_MAGAZINES(100007),
PRODUCT_CATALOGS(100008),
PRODUCT_BOOKLETS(100009),
PRODUCT_ZINES(100010),    PRODUCT_COMIC_BOOKS(100011),   PRODUCT_ART_PRINTS(100012),
PRODUCT_MANGA(100013);



# Element: component
```javascript
{
  "pages": 4,
  "chromaticity": {...},
  "format": {...},
  "material": {...},
  "processing": {...},
  "type": 2
}
```` 

pages
Number of pages in the component (Integer number)
4, 8, 32, to name a few
chromaticity
Chromaticity element which specify the colour space on the front and back
See below
format
Format element which specify the component measurements
See below
material
Material element which specify the component paper stock.
See below
processing
Processing element which specify additional processing such as binding
See below
type
ComponentType
INVALID(0),
CONTENT(1),
COVER(2),
JACKET(3),
BOOKMARK(4),
ENVELOPE (5)


Element: chromaticity
```javascript
{
  "front": 3,
  "back": 3
}
````
front
Colour space on front / outside. (ColorType)
INVALID (0),
HKS (1),
BLACK (2),
PROCESS (3);


back
Colour space on back / inside. (ColorType)
INVALID (0),
HKS (1),
BLACK (2),
PROCESS (3);

Element: format
 "format" : {
    "longEdge" : 210,
    "orientation" : 1,
    "shortEdge" : 99,
    "units": 0
}

longEdge
Component long axis. (Double precision number) in shop’s units 


shortEdge
Component short axis. (Double precision number) in shop’s units 


orientation
(OrientationType)
PORTRAIT(0),
LANDSCAPE(1);


units
The units in which the edges are specified. mm on metric system, inch on imperial.
MM (0),
INCH(1),




# Element: material
```javascript
"material" : {
    "glossiness" : 1,
    “weight" : 170,
    "units" : 1,
    "type" : 4,
    "refinings": [{...}, {...}]
}
````
glossiness
Paper glossiness (MaterialGlossinessType)
NONE(0),
MATT(1),
GLOSS(2),


weight
The weight on one unit (Integer number)


units
Units of weight (PaperWeightUnit)
INVALID(0),
GSM(1),    LIBRA_COVER(2),    LIBRA_TEXT(3),    LIBRA_CARD(4),
type
(MaterialType)
INVALID(0)
SILK(1)
GLOSS(2)    UNCOATED(3)    AFFICHE_PAPER(4)    OUTDOOR_PAPER(5)    ILLUSTRATION_PRINTING_PAPER(6)  PHOTOGRAPHIC_PRINTING_PAPER(7)  POSTCARD_BOARD(8)    NATURAL_PAPER(9)  RECYCLED_PAPER(10)
refinings
List of refining of material such as lamination coating and UV coating.
(MaterialRefining)
See below



# Element: refining
```javascript
"refining": {
  "effect": 2,
  "side": 1,
  "type": 3
}
````
effect
(RefiningEffect)
NONE (0),
MATT_FINISH(1),
GLOSS_FINISH (2),
SILK_FINISH (3),
SOFT_TOUCH (4),
GOLD (5),
SILVER (6),
side
(RefiningSideType)
NONE(0),
FRONT(1),
BACK(2),
FRONT_AND_BACK(3),
OUTSIDE(4),
INSIDE (5)
OUTSIDE_AND_INSIDE(6)
type
(RefiningType)
NONE (0)    ULTRA_VIOLET_COATING(1)
LAMINATION (2),
PROTECTIVE_FOIL (3)
METAL_FOIL (4)    SOFT_PVC_FILM_LAMINATION (5)   ULTRA_VIOLET_SPOT_COATING (6)  
DISPERSION_COATING (7)
BIND_EMBOSSING ( 8)   RELIEF_SPOT_COATING (9)
ULTRA_VIOLET_3D_SPOT_COATING(10)



# Element: processing
```javascript
"processing": {
    "binding": {...},
    "creasing": 0,
    "folding": 0,
    "headTailBand": 1,
    "ribbon": 0,
    "window": 0,
    "feature": 0
}
```
binding
Binding element (map)
See below
creasing
(CreasingType)
NONE(0),    CREASING_NECESSARY(1)


folding
(FoldingType)
FLAT (0),
HALF  (1),
LETTER  (2),
Z  (3),
GATE_OPEN (4),
GATE_CLOSED (5),
CROSS (6),
DOUBLE_PARALLEL (7)
headTailBand
Ratchford (BandType)
NONE(0),
BLACK_AND_WHITE_69WS(1),
WHITE_T117(2),
GREEN_AND_BIEGE_72WS(3),
DARK_BLUE_AND_WHITE_64WS(4),
RED_T105(5),
MAROON_AND_WHITE_66WS(6),
BROWN_AND_BIEGE_58WS(7),
RED_AND_WHITE_56WS(8),
MEDIUM_GREY_T109(9),
YELLOW_T122(10),
BLACK_T108(11),
LIGHT_BLUE_AND_WHITE_634WS(12),
YELLOW_AND_DARK_BLUE_59WS(13),
RED_AND_GREY_55WS(14),
RED_AND_YELLOW_65WS(15),
NAVY_T118(16),
GREEN_AND_BLACK_52WS(17),
PURPLE_AND_WHITE_54WS(18),
BLACK_AND_DARK_GREEN_71WS(19),
GREEN_AND_RED_61WS(20),
RED_AND_BLACK_53WS(21),
YELLOW_AND_BROWN_57WS(22),
YELLOW_AND_BLACK_67WS(23),
GREEN_AND_WHITE_68WS(24),
GREEN_AND_YELLOW_62WS(25),
NAVY_AND_GOLD(26),
ribbon
Ratchford  (RibbonType)
NONE(0),
MAROON(1),
BLACK(2),
DARK_GREEN(3),
BRIGHT_RED(4),
IVORY(5),
WHITE(6),
GOLD(7),
PURPLE(8),
ORANGE(9),
PINK(10),
GREY(11),
BABY_BLUE(12),
BLUE(13),
window
Envelope window (WindowType)
NONE(0),
LEFT(1),
RIGHT(2)
feature
(FeatureType)
INVALID(0),
SUPPLY_FOLDED(1),
SUPPLY_NOT_FOLDED(2),
PERFORATED_ON_TOP(3),
PERFORATED_LEFT(4),
PEEL_AND_SEAL(5)


# Element: binding
```javascript
{
   "type": 2,
   "color": 0,
   "loops": 0,
   "endPaperColor": 0,
   "spineWidth": 7.5,
}
```

type
(BindingType)
NONE(0),
STAPLE_BINDING(1),
PERFECT_BINDING(2),
WIRO_BINDING(3),
LOOP_BINDING(4),
SEWING_BINDING(5),
CALENDAR_BINDING (6)


color
Wiro spiral colour (BindingColorType)
NONE (0),
BLACK (1),
SILVER (2),
WHITE (3),
loops
How many loop holes. (LoopsType)
NONE (0),
TWO (1),
FOUR (2),
endPaperColor
(EndPaperColorType)
NONE(0),
WHITE(1),
BLACK(2);
TBD...
spineWidth
(Double precision number)
In shops units (mm in the UK, inch in the US)

# Element: details
```javascript
 "details": {
   "additionalProjectName": "370260/1",
   "completionType": 3,
   "totalCirculation": 400,
   "dispatchDate": 1579177108174
 }
```
additionalProjectName
Order number. Reference number. (String)


completionType
Urgency of the job. Default value is 4 (Standard)
INVALID(0),
SAME_DAY(1),
EXPRESS(2),
OVERNIGHT(3),
STANDARD(4),
SAVER(5);
totalCirculation
The total number of copies (Integer)



# Element: shipment
```javascript
"shipment": {
   "deliveryItems": [...],
   "senderForLabel": {...},
   "delivery": {...},
   "weight": 1.2
   "units": 1
}
```
deliveryItems
A list of RecipientAddress elements.
(List<RecipientAddress>)
See bellow
senderForLabel
The sender address. 
(Address)
See bellow
delivery
Delivery details.
(Delivery)
See bellow
Weight
The expected weight of the goods. (Double precision number)


units
The units in which the weight is specified. KILOGRAM on metric system, LIBRA on imperial.
KILOGRAM(0),
LIBRA(1),
# Element: RecipientAddress
```javascript
{
  "address": {...},
  "circulation:  100,
  "dispatchDate": 1579693407751,
  "deliveryDate": 1579695818930
}
```
address
Address of recipient (Address)
See bellow
circulation
How many copies to this specific address. (Integer number)


dispatchDate
Epoch date of dispatch (when the boxes are due to be collected by the carrier.) (Long number)
A Unix Timestamp
deliveryDate
Epoch date of delivery (when the boxes are due to arrive at the customer address.) (Long number)
A Unix Timestamp


# Element: address
```javascript
"address": {
      "salutation": "Mr.",
      "firstName": "Rab",
      "surName": "Easton",
      "street1": "31 Holm Gardens",
      "county": "North Lanarkshire",
      "postalCode": "ML4 2PB",
      "city": "Bellshill",
      "country": "GB",
      "telephoneNumber": "07585055748",
      "email": "machinemagazine@mail.com"
}
```
See type ‘Address’

# Element: senderForLabel (Address)
```javascript
"senderForLabel": {
    "salutation": "Mr.",
    "companyName": "Mixam Print",
    "firstName": "Darren",
    "surName": "Elgin",
    "street1": "6 Hercules Way",
    "street2": "Building 1"
    "county": "Hertfordshire",
    "postalCode": "WD25 7GS",
    "city": "Watford",
    "country": "GB",
    "telephoneNumber": "01923 594 040",
    "email": "info@mixam.co.uk"
}
```
See type ‘Address’


 

# Type: Address
```javascript
{
    "salutation": "Mr.",
    "companyName": "Mixam Print",
    "firstName": "Darren",
    "surName": "Elgin",
    "street1": "6 Hercules Way",
    "street2": "Building 1"
    "county": "Hertfordshire",
    "postalCode": "WD25 7GS",
    "city": "Watford",
    "country": "GB",
    "telephoneNumber": "01923 594 040",
    "locationType": 0,
    "email": "info@mixam.co.uk"
}
```
salutation
(SalutationType)
MX("Mx."),
MS("Ms."),
MR("Mr."),
DR("Dr."),
MRS("Mrs"),
PROF("Prof"),
companyName
(String)


firstName
(String)


surName
(String)


street1
(String)


street2
Optional (String) 


street3
Optional (String) 


county
Usually county name. State in the US. (String)


postalCode
Postcode in the UK, zip in US. (String)


city
(String)


country
(String)
“GB”, “US”, “CA” or “AU”
telephoneNumber
(String)


email
(String)


locationType
(AddressLocationType)
RESIDENTIAL(0),
BUSINESS_DOCK(1),
BUSINESS_NO_DOCK(2),
LIMITED_ACCESS(3),
TRADE_SHOW(4),
CONSTRUCTION(5),
FARM(6),


 
# Element: delivery
```javascript
"delivery": {
    "type": "parcel",
    "carrier": "UPS",
    "serviceType": "Next day air",
    "serviceDescription": "By Friday, 17:00",
    "canonicalUri": "UPS_NEXTDAYAIR_2_XCR_Z",
    "cost": 6.50
    "url": "https://mixam.co.uk/spedition/5e2842bc4ed2f62bd2375020"
  }
```

type
(DeliveryType)
PARCEL(0),
PALLET(1),
ENVELOPE(2);


carrier
The name of the carrier (String)
DPD, 2MV, Mini Clipper etc.
serviceType
Usually Next day (in the UK) (String)


serviceDescription
(String)


canonicalUri
A unique identifier of the service (String)


cost
Cost of delivery (Double precision number)


url
Points to a page where collection can be summoned and shipment labels printed. (String)




# Element: File
```javascript
 {
      "type": 0,
      "name": "job372825.pdf",
      "url": "https://s3-eu-...83da8bb6fe8d858d2117/job372825.pdf",
      "checksum": "90be4101398f7f9bc95abe8b1d0f7447",
      "sizeInBytes": 1865517
}
```
type
Which component is associated with this file. (FileType)
ALL(0),
BODY(1),
COVER(2),
DUST_JACKET(3),
HEAD_TO_HEAD(4)
name
Name of file (String)


url
Where to download this file (String)


checksum
MD5 checksum of this file
(String)


sizeInBytes
Size of file (Long number)



Element: export
Optional, applicable only when goods are shipped overseas.
 
"export": {
    "customsValueSum": 100,
    "customsValueCurrency": "USD"
}

customsValueSum
Value of the goods for custom evaluation.
(Integer number)


customsValueCurrency
Currency code  of the above value. 
GBP, USD, CAD, AUD


#JSON Example
```javascript
{
  "version": "3.08",
  "desc": "mixam.job.description",
  "referencedJobNumber": "37663402",
  "author": "Effie Nadiv",
  "dateCreated": 1580388681718,
  "job": {
    "article": {
      "components": [
        {
          "pages": 28,
          "chromaticity": {
            "front": 3,
            "back": 3
          },
          "format": {
            "longEdge": 210.0,
            "orientation": 1,
            "shortEdge": 148.0,
            "units": 0
          },
          "material": {
            "weight": 150,
            "units": 1,
            "refinings": [],
            "type": 1,
            "color": 0
          },
          "processing": {
            "binding": {
              "type": 1,
              "spineWidth": 0.0
            }
          },
          "type": 1
        }
      ],
      "product": 1,
      "subProduct": 0
    },
    "details": {
      "orderId": "5e31a3dc2f231530f33ef3a4",
      "completionType": 2,
      "totalCirculation": 250
    },
    "shipment": {
      "deliveryAddresses": [
        {
          "address": {
            "salutation": "Mr.",
            "firstName": "Charlotte ",
            "surName": "Hall",
            "street1": "Interaction The Vaults",
            "street2": " 1-2 Bartlett Street ",
            "postalCode": "BA12QZ",
            "city": " Bath",
            "county": " Somerset",
            "country": "GB",
            "telephoneNumber": "01225485600",
            "company": "Interaction",
            "locationType": 0
          },
          "circulation": 250,
          "dispatchDate": 1580428800000,
          "deliveryDate": 1580688000000
        }
      ],
      "senderForLabel": {
        "salutation": "Mr.",
        "firstName": "Darren",
        "surName": "Elgin",
        "street1": "6 Hercules Way",
        "postalCode": "WD25 7GS",
        "city": "Watford",
        "county": "Hertfordshire",
        "country": "GB",
        "telephoneNumber": "01923 594 040",
        "email": "info@mixam.co.uk",
        "company": "Mixam Print"
      },
      "delivery": {
        "type": 0,
        "carrier": "Interlink",
        "serviceType": "DPD Next day",
        "serviceDescription": "DPD Next day",
        "canonicalUri": "DPD-DPD_NEXT_DAY-zxa-1",
        "cost": 8.39
      },
      "weight": 16.299999237060547,
      "units": 0
    }
  },
  "files": [
    {
      "type": 0,
      "name": "job376634.pdf",
      "url": "https://s3-eu-west-1.amazonaws.com/files.mixam.com/8472912a7dba3e57ddeb36131ae96726ff3cc5da/job376634.pdf",
      "checksum": "584f4618c4532fbacda1d36d8a0d8338",
      "sizeInBytes": 11437989
    }
  ],
  "export": {
    "customsValueSum": 143.85000610351562,
    "customsValueCurrency": "GBP"
  },
  "price": 143.85000610351562,
  "currencyCode": "GBP"
}
```
#XML Example
```xml
<MxJdf>
    <version>3.08</version>
    <desc>mixam.job.description</desc>
    <referencedJobNumber>37663402</referencedJobNumber>
    <author>Effie Nadiv</author>
    <dateCreated>1580388597661</dateCreated>
    <job>
        <article>
            <components>
                <components>
                    <pages>28</pages>
                    <chromaticity>
                        <front>3</front>
                        <back>3</back>
                    </chromaticity>
                    <format>
                        <longEdge>210.0</longEdge>
                        <orientation>1</orientation>
                        <shortEdge>148.0</shortEdge>
                        <units>0</units>
                    </format>
                    <material>
                        <weight>150</weight>
                        <units>1</units>
                        <refinings/>
                        <type>1</type>
                        <color>0</color>
                    </material>
                    <processing>
                        <binding>
                            <type>1</type>
                            <spineWidth>0.0</spineWidth>
                        </binding>
                    </processing>
                    <type>1</type>
                </components>
            </components>
            <product>1</product>
            <subProduct>0</subProduct>
        </article>
        <details>
            <orderId>5e31a3dc2f231530f33ef3a4</orderId>
            <completionType>2</completionType>
            <totalCirculation>250</totalCirculation>
        </details>
        <shipment>
            <deliveryAddresses>
                <deliveryAddresses>
                    <address>
                        <salutation>Mr.</salutation>
                        <firstName>Charlotte</firstName>
                        <surName>Hall</surName>
                        <street1>Interaction The Vaults</street1>
                        <street2>1-2 Bartlett Street</street2>
                        <postalCode>BA12QZ</postalCode>
                        <city>Bath</city>
                        <county>Somerset</county>
                        <country>GB</country>
                        <telephoneNumber>01225485600</telephoneNumber>
                        <company>Interaction</company>
                        <locationType>0</locationType>
                    </address>
                    <circulation>250</circulation>
                    <dispatchDate>1580428800000</dispatchDate>
                    <deliveryDate>1580688000000</deliveryDate>
                </deliveryAddresses>
            </deliveryAddresses>
            <senderForLabel>
                <salutation>Mr.</salutation>
                <firstName>Darren</firstName>
                <surName>Elgin</surName>
                <street1>6 Hercules Way</street1>
                <postalCode>WD25 7GS</postalCode>
                <city>Watford</city>
                <county>Hertfordshire</county>
                <country>GB</country>
                <telephoneNumber>01923 594 040</telephoneNumber>
                <email>info@mixam.co.uk</email>
                <company>Mixam Print</company>
            </senderForLabel>
            <delivery>
                <type>0</type>
                <carrier>Interlink</carrier>
                <serviceType>DPD Next day</serviceType>
                <serviceDescription>DPD Next day</serviceDescription>
                <canonicalUri>DPD-DPD_NEXT_DAY-zxa-1</canonicalUri>
                <cost>8.39</cost>
            </delivery>
            <weight>16.299999237060547</weight>
            <units>0</units>
        </shipment>
    </job>
    <files>
        <files>
            <type>0</type>
            <name>job376634.pdf</name>
            <url>https://s3-eu-west-1.amazonaws.com/files.mixam.com/8472912a7dba3e57ddeb36131ae96726ff3cc5da/job376634.pdf</url>
            <checksum>584f4618c4532fbacda1d36d8a0d8338</checksum>
            <sizeInBytes>11437989</sizeInBytes>
        </files>
    </files>
    <export>
        <customsValueSum>143.85000610351562</customsValueSum>
        <customsValueCurrency>GBP</customsValueCurrency>
    </export>
    <price>143.85000610351562</price>
    <currencyCode>GBP</currencyCode>
</MxJdf>
```

