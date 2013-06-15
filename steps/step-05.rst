Step A5 - filter by distance
============================
Calculate distances; only print nearby parks.

::

    import pyproj
    geod = pyproj.Geod(ellps='WGS84')

    def calculate_hikers(cities_layer, population, parks_data):
        max_distance = 50000  # 50 Km
        for i in range(cities_layer.GetFeatureCount()):
            city = cities_layer.GetFeature(i)
            # ...
            city_centroid = city_geom.Centroid()
            city_centroid.Transform(stereo70_to_wgs84)
            for park in parks_data:
                park_centroid = park['centroid']
                (angle1, angle2, distance) = geod.inv(
                    city_centroid.GetX(), city_centroid.GetY(),
                    park_centroid.GetX(), park_centroid.GetY())
                if distance < max_distance:
                    print '->', park['name'], distance
