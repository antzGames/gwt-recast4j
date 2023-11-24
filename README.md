![Build Status](https://img.shields.io/github/actions/workflow/status/ppiastucki/recast4j/gradle.yml?branch=main&logo=github)
![Repo Size](https://img.shields.io/github/repo-size/ppiastucki/recast4j.svg?colorB=lightgray)
[![Maven Central](https://img.shields.io/maven-central/v/org.recast4j/recast.svg?label=maven%20central)](https://search.maven.org/search?q=g:org.recast4j)
![Languages](https://img.shields.io/github/languages/top/ppiastucki/recast4j)
![Dependencies](https://img.shields.io/librariesio/github/ppiastucki/recast4j)

GWT Compatible - Recast4j
=========================

Java Port of Recast and Detour navigation mesh toolset that is GWT compatible.

![screenshot of a navmesh baked with the sample program](/recast-demo/screenshot.png?raw=true)

## How to use in your libGDX project

Add the `recast4jVersion=master-SNAPSHOT` to your `gradle.properties` file.

FYI: Antz uses the `gwt_migration_antz-SNAPSHOT` branch for latest fixes, bugs, new features.

Add the following in your `core` project's `gradle.build`:
```
dependencies {
  api "com.github.antzGames.gwt-recast4j:recast:$recast4jVersion"
  api "com.github.antzGames.gwt-recast4j:detour:$recast4jVersion"
  api "com.github.antzGames.gwt-recast4j:detour-crowd:$recast4jVersion"
}
```

Add the following in your `html` project's `gradle.build`:

```
dependencies {
  implementation "com.github.antzGames.gwt-recast4j:recast:$recast4jVersion"
  implementation "com.github.antzGames.gwt-recast4j:detour:$recast4jVersion"
  implementation "com.github.antzGames.gwt-recast4j:detour-crowd:$recast4jVersion"

  implementation "com.github.antzGames.gwt-recast4j:recast:$recast4jVersion:sources"
  implementation "com.github.antzGames.gwt-recast4j:detour:$recast4jVersion:sources"
  implementation "com.github.antzGames.gwt-recast4j:detour-crowd:$recast4jVersion:sources"
}
```

Add the following to your `GdxDefinition.gwt.xml` file in your `html` project:

```
    <inherits name="recast4j_detour" />
    <inherits name="recast4j_detour_crowd" />
    <inherits name="recast4j_recast" />
```

## Recast

Recast is state of the art navigation mesh construction toolset for games.

Recast is...
* 🤖 **Automatic** - throw any level geometry at it and you will get a robust navmesh out
* 🏎️ **Fast** - swift turnaround times for level designers
* 🧘 **Flexible** - easily customize the navmesh generation and runtime navigation systems to suit your specific game's needs.

Recast constructs a navmesh through a multi-step rasterization process:

1. First Recast voxelizes the input triangle mesh by rasterizing the triangles into a multi-layer heightfield. 
2. Voxels in areas where the character would not be able to move are removed by applying simple voxel data filters.
3. The walkable areas described by the voxel grid are then divided into sets of 2D polygonal regions.
4. The navigation polygons are generated by triangulating and stiching together the generated 2d polygonal regions.

## Detour

Recast is accompanied by Detour, a path-finding and spatial reasoning toolkit. You can use any navigation mesh with Detour, but of course the data generated with Recast fits perfectly.

Detour offers a simple static navmesh data representation which is suitable for many simple cases.  It also provides a tiled navigation mesh representation, which allows you to stream of navigation data in and out as the player progresses through the world and regenerate sections of the navmesh data as the world changes.

More information about [Recast and Detour](https://github.com/recastnavigation/recastnavigation)

## Java Version
### How To Use
The API is kept as close to https://github.com/recastnavigation/recastnavigation as possible so most of the information and hints apply to recast4j too.
You can find a lot of examples in tests e.g.
- building a nav mesh from obj files: https://github.com/ppiastucki/recast4j/blob/master/detour/src/test/java/org/recast4j/detour/RecastTestMeshBuilder.java
- finding a path: https://github.com/ppiastucki/recast4j/blob/master/detour/src/test/java/org/recast4j/detour/FindPathTest.java#L94
- persisting a nav mesh: https://github.com/ppiastucki/recast4j/blob/master/detour/src/test/java/org/recast4j/detour/io/MeshSetReaderWriterTest.java
- dynamic nav mesh: https://github.com/ppiastucki/recast4j/blob/master/detour-dynamic/src/test/java/org/recast4j/dynamic/DynamicNavMeshTest.java
### Java Version Enhancements
#### recast
- out-of-the-box support for multi-threaded builds
- support for rasterizing filled volumes: sphere, capsule and box
#### detour
- finding random points constrained by a cricle
#### detour-tile-cache
- more compact file format due to reduced data structures and better compression with LZ4
#### detour-extras
- simple tool to import navmeshes created with [A* Pathfinding Project](https://arongranberg.com/astar/)
#### detour-dynamic
- robust support for dynamic nav meshes combining pre-built voxels with dynamic objects which can be freely added and removed

### Building from Source

All the modules can be built with a single gradle command:
```
./gradlew clean build shadow
```

Once the build is completed, the recast-demo application can be run as follows:
```
java -jar ./recast-demo/build/libs/recast-demo-1.5.6-SNAPSHOT-all.jar
```

### Binaries

#### Releases
Recast4j releases are available in Maven Central Repository.
Maven:
```
<dependency>
	<groupId>org.recast4j</groupId>
	<artifactId>recast</artifactId>
	<version>1.5.5</version>
</dependency>
<dependency>
	<groupId>org.recast4j</groupId>
	<artifactId>detour</artifactId>
	<version>1.5.5</version>
</dependency>
<dependency>
	<groupId>org.recast4j</groupId>
	<artifactId>detour-crowd</artifactId>
	<version>1.5.5</version>
</dependency>
<dependency>
	<groupId>org.recast4j</groupId>
	<artifactId>detour-tile-cache</artifactId>
	<version>1.5.5</version>
</dependency>
<dependency>
	<groupId>org.recast4j</groupId>
	<artifactId>detour-extras</artifactId>
	<version>1.5.5</version>
</dependency>
<dependency>
	<groupId>org.recast4j</groupId>
	<artifactId>detour-dynamic</artifactId>
	<version>1.5.5</version>
</dependency>
```
Gradle:
```
implementation 'org.recast4j:recast:1.5.5'
implementation 'org.recast4j:detour:1.5.5'
implementation 'org.recast4j:detour-crowd:1.5.5'
implementation 'org.recast4j:detour-tile-cache:1.5.5'
implementation 'org.recast4j:detour-extras:1.5.5'
implementation 'org.recast4j:detour-dynamic:1.5.5'
```

## License

Recast & Detour is licensed under ZLib license, see License.txt for more information.
