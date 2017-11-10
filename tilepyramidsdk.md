## Tile Pyramid SDK Reference

The Tile Pyramid SDK requires that the following interfaces are implemented.

| Interface | Description |
| -- | -- |
| [**IColorMap**](#IColorMapInterface) | Used to retrieve color data.|
| **[IDemPlateFileGenerator](#IDemPlateFileGeneratorInterface)**| Used to generate plate files for DEM tiles (plate files are single files containing all or part of a tile pyramid for easy copying, sharing and backup).
| [**IDemTileSerializer**](#IDemTileSerializerInterface)| Used to serialize and deserialize (save and load) DEM data.
| [**IElevationMap**](#IElevationMapInterface)| Used to retrieve elevation data.
| [**IGrid**](#IGridInterface)| Used to read source data into a source grid which can be accessed using UV or XY co-ordinates.
| **[IImageTileSerializer](#IImageTileSerializerInterface)**| Used to serialize and deserialize (save and load) image data.
| **[IPlateFileGenerator](#IPlateFileGeneratorInterface)**| Used to generate plate files for image tiles (plate files are single files containing all or part of a tile pyramid for easy copying, sharing and backup).
| [**IProjectionGridMap**](#IProjectionGridMapInterface)| Used to query the data grid based on the projection.
| [**ITileCreator**](#ITileCreatorInterface)| Used to build the tile pyramids.

The following are the core classes of the SDK, and source code is provided for all of them. They are encapsulated in the **Sdk.Core** project.


| Class | Description |
| -- | -- |
| **Boundary**| Defines a bounding rectangle.
| **Constants**| Defines a range of global constants.
| **<a name="DataColorMap">DataColorMap**| Implements [**IColorMap**](#IColorMapInterface), to generate color pixels corresponding to latitude and longitude from the source grid.
| **<a name="DataGrid">DataGrid**| Implements [**IGrid**](#IGridInterface), providing a two dimensional array of data.
| **<a name="DemPlateFileGenerator">DemPlateFileGenerator**| Implements **[IDemPlateFileGenerator](#IDemPlateFileGeneratorInterface)**, to produce a single file containing all the DEM data tiles.
| **<a name="DemTileSerializer">DemTileSerializer**| Implements [**IDemTileSerializer**](#IDemTileSerializerInterface) to save and load DEM tiles on the file system.
| **Enums**| Defines the global enumerations.
| **<a name="EquirectangularGridMap">EquirectangularGridMap**| Implements [**IProjectionGridMap**](#IProjectionGridMapInterface), using equirectangular projection.
| **Helper**| Defines a few utility methods related to unit conversions.
| **<a name="ImageColorMap">ImageColorMap**| Implements [**IColorMap**](#IColorMapInterface), and references [**IProjectionGridMap**](#IProjectionGridMapInterface)..
| **<a name="ImageGrid">ImageGrid**| Implements [**IGrid**](#IGridInterface), providing a two dimensional array of image data.
| **<a name="ImageTileSerializer">ImageTileSerializer**| Implements [**IImageTileSerializer**](#IImageTileSerializerInterface) to save and load image tiles on file system.
| **<a name="MercatorDemTileCreator">MercatorDemTileCreator**| Implements [**ITileCreator**](#ITileCreatorInterface) to create Mercator DEM tiles. Refer also to [Appendix I: DEM Tile Data](#Appendix).
| **<a name="MercatorTileCreator">MercatorTileCreator**| Implements [**ITileCreator**](#ITileCreatorInterface) to create Mercator image tiles.
| **<a name="MultipleDemPlateFileGenerator">MultipleDemPlateFileGenerator**| Implements **[IDemPlateFileGenerator](#IDemPlateFileGeneratorInterface)**, to produce multiple DEM plate files containing DEM data tiles.
| **MercatorPlateFileDetails**| Used to calculate and store the details of multiple plate files.
| **<a name="MultiplePlateFileGenerator">MultiplePlateFileGenerator**| Implements **[IPlateFileGenerator](#IPlateFileGeneratorInterface)** to produce multiple plate files containing image tiles.
| **<a name="MultiTileCreator">MultiTileCreator**| Implements [**ITileCreator**](#ITileCreatorInterface) for different tile creator instances.
| **OctTileMap**| Defines an octahedral tile map.
| **PlateFile**| Defines utility methods for plate file operations.
| **<a name="PlateFileGenerator">PlateFileGenerator**| Implements [**IPlateFileGenerator**](#IPlateFileGeneratorInterface), used to create plate files.
| **PlateFileHelper**| Defines a range of utility methods for plate files.
| **Tile**| Simple class holding tile coordinates.
| **<a name="TileChopper">TileChopper**| Implements [**ITileCreator**](#ITileCreatorInterface) to create image tiles without changing the projection.
| **TileCreatorFactory**| Creates an image or DEM tile creator instance for the specified projection type.
| **TileGenerator**| This class contains the main control/workflow code for the tile generation process.
| **TileHelper**| Defines a range of utility methods for tiles and bitmaps.
| **<a name="ToastDemTileCreator">ToastDemTileCreator**| Implements [**ITileCreator**](#ITileCreatorInterface) to create Toast DEM tiles. Refer also to [Appendix I: DEM Tile Data](#Appendix).
| **ToastHelper**| Helper class, in particular working with Toast coordinates.
| **<a name="ToastTileCreator">ToastTileCreator**| Implements [**ITileCreator**](#ITileCreatorInterface) to create Toast image tiles.
| **WtmlCollection**| Defines a new Wtml collection, a WorldWide Telescope data file.

## IColorMap Interface

The **IColorMap** interface is used to retrieve color data, and exposes the following methods. It does not inherit from another interface.

| Method | Description |
| -- | -- |
| [**GetColor**](#IColorMapGetColor)| Retrieves the color corresponding to a longitude and latitude. |


#### Implemented in Classes

*   [**DataColorMap**](#DataColorMap)
*   [**ImageColorMap**](#ImageColorMap)

### IColorMap.GetColor

The **GetColor** method retrieves the color corresponding to a longitude and latitude.

#### Syntax

    Color GetColor(
      double  longitude,
      double  latitude
    );

#### Parameters

longitude
  Specifies longitude in decimal degrees.
latitude
  Specifies latitude in decimal degrees.

#### Return Values

The method returns a **Color** object, containing the color of the pixel at the given latitude and longitude.

#### Remarks

Typically the color returned comes from the source image. Note the order of the parameters, longitude first.

## IDemPlateFileGenerator Interface

The **IDemPlateFileGenerator** interface is used to generate plate files for DEM tiles (plate files are single files containing all or part of a tile pyramid for easy copying, sharing and backup). It does not inherit from another interface.


| Method | Description
| -- | -- |
| [**CreateFromDemTile**](#IDemPlateFileGeneratorCreateFromDemTileSerializer)| Used to create a plate file from a DEM tile pyramid. |


#### Properties


| Property | Type | Get/Set | Description
| -- | -- | -- | -- |
| **TilesProcessed**| **long**| Get only.| Number of tiles for the level that have been processed.


#### Implemented in Classes

*   [**DemPlateFileGenerator**](#DemPlateFileGenerator)
*   [**MultipleDemPlateFileGenerator**](#MultipleDemPlateFileGenerator)


### IDemPlateFileGenerator.CreateFromDemTile

The **CreateFromDemTile** method is used to create a plate file from a DEM tile pyramid.

#### Syntax

    void CreateFromDemTile(
      IDemTileSerializer  serializer
    );

#### Parameters

serializer
  Specifies the [**IDemTileSerializer**](#IDemTileSerializerInterface) object.

#### Return Values

The method does not returns a value.

#### Remarks

None.

## IDemTileSerializer Interface

The **IDemTileSerializer** interface is used to serialize and deserialize (save and load) DEM data, and exposes the following methods. It does not inherit from another interface.


| Method | Description
| -- | -- |
| [**Deserialize**](#IDemTileSerializerDeserialize)| Deserializes a binary object from the file system.
| [**Serialize**](#IDemTileSerializerSerialize)| Serializes the binary file to the file system.

#### Implemented in Class

*   [**DemTileSerializer**](#DemTileSerializer)

### IDemTileSerializer.Deserialize

The **Deserialize** method deserializes (loads) a DEM tile from the file system.

#### Syntax

    short[] Deserialize(
      int  level,
      int  tileX,
      int  tileY
    );

#### Parameters

level
  Specifies the tile level, from zero to the maximum level for the data.
tileX
  Specifies the X index of the tile in the tile pyramid.
tileY
  Specifies the Y index of the tile in the tile pyramid.

#### Return Values

The method returns an array of **short** values, containing the binary data.

#### Remarks

The size of a DEM tile is fixed depending on the projection, refer to the remarks for [**Serialize**](#IDemTileSerializerSerialize).

### IDemTileSerializer.Serialize

The **Serialize** method serializes (saves) the DEM tile to the file system.

#### Syntax

    void Serialize(
      short[]  tile,
      int  level,
      int  tileX,
      int  tileY
    );

#### Parameters

tile
  Specifies the array of values that make up the DEM tile.
level
  Specifies the tile level, from zero to the maximum level for the data.
tileX
  Specifies the X index of the tile in the tile pyramid.
tileY
  Specifies the Y index of the tile in the tile pyramid.4

#### Return Values

The method does not return a value.

#### Remarks

The size of a DEM tile is fixed depending on the projection, for Mercator it is 1089 values (33 rows of 33), organized by rows. Refer to the **MercatorDemTileCreator** class.

 For Toast it is 513 values, these values are not in a perfect grid. Refer to the static tables listed first in the **ToastDemTileCreator** class.

## IElevationMap Interface

The **IElevationMap** interface is used to retrieve elevation data, and exposes the following methods. It does not inherit from another interface.


| Method | Description
| -- | -- |
| [**GetElevation**](#IElevationMapGetElevation)| Retrieves the elevation corresponding to the longitude and latitude.

#### Implemented in Class

This interface is implemented in the **ShadedReliefColorMap** class in the **[SpecificRegionDataSet](worldwidetelescopetilepyramidsdksamples.html)** sample.


### IElevationMap.GetElevation

The **GetElevation** method retrieves the elevation corresponding to the longitude and latitude.

#### Syntax

    short GetElevation(
      double  longitude,
      double  latitude
    );

#### Parameters

longitude
  Specifies longitude in decimal degrees.
latitude
  Specifies latitude in decimal degrees.

#### Return Values

The method returns a **short**, containing the elevation value.

#### Remarks

Note the order of the parameters, longitude first.

## IGrid Interface

The **IGrid** interface is used to read source data into a source grid which can be accessed using UV or XY co-ordinates. It does not inherit from another interface.


| Method | Description
| -- | -- |
| [**GetValue**](#IGridGetValue)| Retrieves the value contained at the specified coordinate.
| [**GetValueAt**](#IGridGetValueAt)| Retrieves the value contained at the specified pixel location.
| [**GetXIndex**](#IGridGetXIndex)| Retrieves the X pixel index for the given coordinate.
| **[GetYIndex](#IGridGetYIndex)**| Retrieves the Y pixel index for the given coordinate.


#### Properties


| Property | Type | Get/Set | Description
| -- | -- | -- | -- |
| **Height**| **int**| Get/Set| Height of the grid.
| **Width**| i**nt**| Get only| Width of the grid.

#### Implemented in Classes

*   [**DataGrid**](#DataGrid)
*   [**ImageGrid**](#ImageGrid)

### IGrid.GetValue



The **GetValue** method retrieves the value contained at the specified coordinate.

#### SySyntax

    double GetValue(
      double  u,
      double  v
    );

#### Parameters

u
  Specifies u coordinate.
v
  Specifies v coordinate.

#### Return Values

The method returns a **double**, containing the value for the given coordinate.

#### Remarks

UV coordinates are floating point in the range 0 to 1\. The top left hand corner of the map is 0,0.

### IGrid.GetValueAt

The **GetValueAt** method retrieves the value contained at the specified pixel location.

#### Syntax

    double GetValueAt(
      int  i,
      int  j
    );

#### Parameters

i
  Specifies X index.
j
  Specifies Y i<span class="style1">ndex</span>.

#### Return Values

The method returns a **double,** containing the value.

#### Remarks

These coordinates are in pixels, from 0 to the full width or height of the map. The top left hand corner of the map is 0,0.


### IGrid.GetXIndex

The **GetXIndex** method retrieves the X pixel index for the given u coordinate.

#### Syntax

    int GetXIndex(
      double  u
    );

#### Parameters

u
  Specifies u coordinate  in decimal degrees.

#### Return Values

The method returns an **int**, containing the X pixel value for the given coordinate.

#### Remarks

The U coordinate is in the range 0 to 1.




### IGrid.GetYIndex



The **GetYIndex** method retrieves the Y pixel index for the given V coordinate.

#### Syntax

    int GetYIndex(
      double  v
    );

#### Parameters

v
  Specifies v coordinate in decimal degrees.

#### Return Values

The method returns an **int**, containing the Y pixel value for the given coordinate.

#### Remarks

The V coordinate is in the range 0 to 1.

## IImageTileSerializer Interface



The **IImageTileSerializer** interface is used to serialize and deserialize (save and load) image data, and exposes the following methods.


| Method | Description
| -- | --
| [**Deserialize**](#IImageTileSerializerDeserialize)| Deserializes an image from the file system.
| [**Serialize**](#IImageTileSerializerSerialize)| Serializes the image to the file system.


#### Implemented in Class

[**ImageTileSerializer**](#ImageTileSerializer)

### IImageTileSerializer.Deserialize



The **Deserialize** method deserializes (loads) an image from the file system.

#### Syntax

    Bitmap Deserialize(
      int  level,
      int  tileX,
      int  tileY
    );

#### Parameters

level
  Specifies the tile level, from zero to the maximum level for the data.
tileX
  Specifies the X index of the tile in the tile pyramid.
tileY
  Specifies the Y index of the tile in the tile pyramid.

#### Return Values

The method returns a **Bitmap**, containing the binary image.

#### Remarks

Indexes of the tile pyramid are zero based. The size of an image tile is fixed at 256 x 256 pixels.



### IImageTileSerializer.Serialize



The **Serialize** method serializes (saves) the tile image to the file system.

#### Syntax

    void Serialize(
      Bitmap  tile,
      int  level,
      int  tileX,
      int  tileY
    );`

#### Parameters

tile
  Specifies the Bitmap for the tile.
level
  Specifies the tile level, from zero to the maximum level for the data.
tileX
  Specifies the X index of the tile in the tile pyramid.
tileY
  Specifies the Y index of the tile in the tile pyramid.

#### Return Values

The method does not return a value.

#### Remarks

Indexes of the tile pyramid are zero based. The size of an image tile is fixed at 256 x 256 pixels.


## IPlateFileGenerator Interface

The **IPlateFileGenerator** interface is used to generate plate files for image tiles (plate files are single files containing all or part of a tile pyramid for easy copying, sharing and backup).  It does not inherit from another interface.




| Method | Description
| -- | --
| [**CreateFromImageTile**](#IPlateFileGeneratorCreateFromImageTile)| Used to create a plate file from an image tile pyramid.


#### Properties


| Property | Type | Get/Set | Description
| -- | -- | -- |
| **TilesProcessed**| **long**| Get only.| Number of tiles for the level that have been processed.


#### Implemented in Classes

*   [**PlateFileGenerator**](#PlateFileGenerator)
*   [**MultiplePlateFileGenerator**](#MultiplePlateFileGenerator)


### IPlateFileGenerator.CreateFromImageTile

The **CreateFromImageTile** method is used to create a plate file from an image tile pyramid.

#### Syntax

    void CreateFromImageTile(
      IImageTileSerializer  serializer
    );

#### Parameters

serializer
  Specifies the [**IImageTileSerializer**](#IImageTileSerializerInterface) object.

#### Return Values

The method does not returns a value.

#### Remarks

The image pyramid must be created before a plate file can be generated. Plate files are single files that make it easier to send or archive the tile pyramid.


## IProjectionGridMap Interface



The **IProjectionGridMap** interface is used to query the data grid based on the projection. It does not inherit from another interface.


| Method | Description
| -- | -- |
| [**GetValue**](#IProjectionGridMapGetValue)| Retrieves the value contained at the specified coordinate.
| [**GetXIndex**](#IProjectionGridMapGetXIndex)| Retrieves the X pixel index for the given coordinate.
| **[GetYIndex](#IProjectionGridMapGetYIndex)**| Retrieves the Y pixel index for the given coordinate.
| **[IsInRange](#IProjectionGridMapIsInRange)**| Retrieves a Boolean indicating whether a given coordinate falls within the scope of the map.


#### Properties


| Property | Type | Get/Set | Description
| -- | -- | -- | -- |
| **InputBoundary**| **Boundary**| Get only| Bounding box of the map.
| **InputGrid**| **[IGrid](#IGridInterface)**| Get only| The source grid for the map.


#### Implemented in Class

*   [**EquirectangularGridMap**](#EquirectangularGridMap)

### IProjectionGridMap.GetValue



The **GetValue** method retrieves the value contained at the specified coordinate.

#### Syntax

  double GetValue(
    double  longitude,
    double  latitude
  );

#### Parameters

longitude
  Specifies longitude  in decimal degrees.
latitude
  Specifies latitude  in decimal degrees.

#### Return Values

The method returns a **double**, containing the value for the given coordinate, depending on the projection.

#### Remarks

Note the order of the parameters, longitude first.

### IProjectionGridMap.GetXIndex


The **GetXIndex** method retrieves the X pixel index for the given longitude.

#### Syntax

    int GetXIndex(
      double  longitude
    );

#### Parameters

longitude
  Specifies longitude in decimal degrees.

#### Return Values

The method returns an **int**, containing the X pixel value for the given longitude, depending on the projection.

#### Remarks

None.

### IProjectionGridMap.GetYIndex

The **GetYIndex** method retrieves the Y pixel index for the given latitude.

#### Syntax

    int GetYIndex(
      double  latitude
    );

#### Parameters

latitude
  Specifies latitude in decimal degrees.

#### Return Values

The method returns an **int**, containing the Y pixel value for the given latitude, depending on the projection.

#### Remarks

None.

### IProjectionGridMap.IsInRange

The **IsInRange** method retrieves a Boolean indicating whether a given coordinate falls within the scope of the map.

#### SySyntax

    bool IsInRange(
      double  longitude,
      double  latitude
    );

#### Parameters

longitude
  Specifies longitude  in decimal degrees.
latitude
  Specifies latitude  in decimal degrees.

#### Return Values

The method returns a **bool**.

#### Remarks

Note the order of the parameters, longitude first.

## ITileCreator Interface

The **ITileCreator** interface is used to build the tile pyramids, and exposes the following methods. It does not inherit from another interface.


| Method | Description
| -- | -- |
| [**Create**](#ITileCreatorCreate)| Creates tiles of the pyramid at the specified level.
| [**CreateParent**](#ITileCreatorCreateParent)| Create tiles of the pyramid at the parent of the specified level.


#### Properties

| Property | Type | Get/Set | Description
| -- | -- | -- | -- |
| **ProjectionType**| **ProjectionTypes**| Get only.| Specifies or retrieves the projection type, one of:
**Toast**
**Mercator**


#### Implemented in Classes

*   [**ToastTileCreator**](#ToastTileCreator)
*   [**MercatorTileCreator**](#MercatorTileCreator)
*   [**ToastDemTileCreator**](#ToastDemTileCreator)
*   [**MercatorDemTileCreator**](#MercatorDemTileCreator)
*   [**MultiTileCreator**](#MultiTileCreator)
*   [**TileChopper**](#TileChopper)

### ITileCreator.Create

The **Create** method creates tiles of the pyramid at the specified level.

#### Syntax

    void Create(
      int  level,
      int  tileX,
      int  tileY
    );

#### Parameters

level
  Specifies the tile level, from zero to the maximum level for the data.
tileX
  Specifies the X index of the tile in the tile pyramid.
tileY
  Specifies the Y index of the tile in the tile pyramid.

#### Return Values

This method does not return a value.

#### Remarks

If the input to this method was **Create**(N,X,Y), the output would be the tile with coordinates (X,Y) at level N.

### ITileCreator.CreateParent

The **CreateParent** method creates tiles for the parent of the specified level.

#### Syntax

    void CreateParent(
      int  level,
      int  tileX,
      int  tileY
    );

#### Parameters

level
  Specifies the tile level, from zero to the maximum level for the data.
tileX
  Specifies the X index of the tile in the tile pyramid.
tileY
  Specifies the Y index of the tile in the tile pyramid.

#### Return Values

This method does not return a value.

#### Remarks

If the input to this method was **CreateParent**(N,X,Y), the output would be the tile with coordinates (X/2,Y/2) at level N-1.
