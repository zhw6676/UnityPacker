# UnityPacker

UnityPacker is a collection of a library and small command line tools that can create, unpack and inspect `UnityPackage` files without a Unity installation. It is great for automated builds of Unity tools.

Usage is very simple:

    ./UnityPack *directory to pack* *destination pack name*
    ./UnityUnpack *pack name* *directory to unpack to*
    
For example:

    ./UnityPack . Package
    
Will produce a `Package.unitypackage` from the contents current directory recursively in the current directory.

    ./UnityUnpack Package.unitypackage .

Will unpack the `Package.unitypackage` to the working directory, with proper directory structure.

+ When used with `respectMeta` option, packer will maintain prefab components 
and even complete scenes if they are included in the directory.

+ It will maintain meta files through packing and unpacking. You can include a meta file generated by unity.
If no meta file exists for a file, it will be automatically generated.

+ It can omit more using the `extensions` option. 

+ It can omit whole directories with the `directories` option.

+ Sizes of the packages exported from Unity itself and UnityPacker are usually the same.

# Full usage

	./UnityPack . MyAssets Assets/MyAssets "gitignore,md,exe,dll" ".git"

Such a run will create a file called `MyAssets.unitypackage` with the contents of this directory,
omitting files with extensions `gitignore, md, exe, dll` and the directory `.git`. When imported
by unity, all files will be put in `MyAssets` folder in project. The path starts from unity project
root, so if it doesn't start with `Assets/` it won't show up in the editor!

	./UnityUnpack MyAssets.unitypackage .

Such a run will extract the contents of the unitypackage with proper directory structure to
the working directory.

*Was tested on Unity 2017.2.0f3 and 5.5 with packages from both Mac and Linux hosts.*
