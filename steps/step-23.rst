Step 23
=======
Save layer with park densities.

::

    def calculate_density(parks_layer, densities_layer, hikers):
        densities_layer_defn = densities_layer.GetLayerDefn()
        for i in range(parks_layer.GetFeatureCount()):
            # ...
            park_out = ogr.Feature(densities_layer_defn)
            park_out.SetField('name', name)
            park_out.SetField('visitors', people)
            park_out.SetField('density', density)
            park_out.SetGeometry(park_geom)
            densities_layer.CreateFeature(park_out)


    def main():
        # ...
        densities = shp_driver.CreateDataSource('output/densities.shp')
        densities_layer = densities.CreateLayer('layer', stereo70)
        densities_layer.CreateField(ogr.FieldDefn('name', ogr.OFTString))
        densities_layer.CreateField(ogr.FieldDefn('visitors', ogr.OFTInteger))
        densities_layer.CreateField(ogr.FieldDefn('density', ogr.OFTReal))
        calculate_density(parks_layer, densities_layer, hikers)
        densities.Destroy()
        # ...
