# Avatar assets and templates for TON Metaspace

This contains some useful working files for editing avatars for [TON Metaspace](https://tonmetaspace.org).

**IMPORTANT: If you are cloning this repo, _you MUST first install [GitLFS](https://git-lfs.github.com/)_ or else many of the files will not work.**

Depending on how involved you'd like to get in the avatar creation process, you might choose to simply 're-skin' the existing avatar by painting your own texture maps, or create your own fully custom 3D model.

# Types of Avatars

There are three main types of avatars in Metaspace: full-body avatars(coming-soom), half-body avatars, and non-rigged avatars.

Full-body and half-body avatars are both rigged, with the half-body avatars having a pared down skeleton that only includes a spine from the hips up to the head and a pair of hands. Rigged avatars have specific requirements in order to work. More details in the [Creating New Avatars] section.

Non-rigged avatars can be pretty much any model without a rig.

![avatars](/avatars.png)

# Customizing Avatars for Metaspace

Avatars for Metaspace are glTF 3D binary models with a skeleton. There are several mechanics for customizing your Metaspace avatar, which, if you are signed in, will stay saved in the ‘My Avatars’ collection. You can also choose from ‘Featured’ avatars that have been made by other users and published for reuse. You will be given the option to select an avatar on your first time using Metaspace. If you want to change your avatar after that point:

1. Enter a Metaspace
2. Select the ‘People’ list icon in the top right corner of the screen
3. By your name, you will see a pencil icon. Click this icon to open the avatar selection screen
4. Click the ‘Browse Avatars’ button
5. From here, you can see a list of your own avatars, but you can toggle between your avatars and Featured avatars from the top tab. You can also link to a custom avatar glb from this screen.

![mrproton](/mrproton.png)

# Customizing textures

The most straightforward way to customize an avatar for Metaspace is to upload a custom texture set. This is the option that you’ll have available when you click the ‘Create Avatar’ button.

The preview will be updated as you add textures. You do not need to include all textures - any combination of maps are supported. Each of the slots listed handle a different texture type.

# Create Avatar

In the avatar browser, you will see a button as the first option called “Create Avatar”. This will allow you to upload a .glb file to Alakazam as a new avatar. As these avatars get saved to the back-end, you will be able to use Option 1 to choose this new avatar in subsequent visits, even if your cookies get cleared.

![create](/create.png)

# Art Pipeline for [glTF](https://www.khronos.org/gltf/)

Authoring content for a new file format can be exciting, liberating, and at the same time scary. To be the most efficient and avoid frustration, it helps to understand the format's requirements. To help achieve that, I am going to walk through several paths for authoring content in the glTF format as well as outline specific settings to maximize your success. I will touch on both free and commercial software packages to ensure everyone has a path into glTF, but first let's outline a few important concepts.

# Overview of the Avatar Pipeline

![glb](https://www.khronos.org/assets/uploads/blogs/2018-blog-art-pipeline-for-gltf-1.jpg)

# Material Specifications

glTF will support Specular-Glossiness materials. With that in mind, my examples will use Metallic-Roughness materials to ensure the most flexible assets possible. If you are new to authoring textures for PBR materials, there is a [comprehensive guide](https://www.allegorithmic.com/pbr-guide) on the subject available from [Allegorithmic](https://www.allegorithmic.com/) that is a great place to start.

# Mesh Considerations

Because glTF is designed for run-time delivery, meshes should be created with real-time rendering guidelines in mind.

- Optimize your triangle count budgets to perform well on the web and on mobile.
- Assign only one material per sub-mesh.
- Combine sub-meshes where possible to reduce draw calls.

Otherwise, you can create your model in any package you prefer. The tools that can export a model and textures into the glTF format at this point are 3ds Max, Blender, and Substance Painter with more exporters coming soon. If your model was not created in one of these packages (or you are using Substance Painter to export) you will need to save your model into an exchange format that can be imported into these packages such as COLLADA.

# Authoring Tools vs. Command Line Converters

In this post I am touching on authoring tools such as 3ds Max, Blender, and Substance Painter even though there are several command line conversion tools available for glTF. There are two main reasons for this and the first one is speed. If I am already using an authoring tool, having a path to glTF right from the tool without needing to run it through a converter will speed my process. The other reason, which is the more important consideration, is to ensure that the mesh and textures I author are translated into the format correctly. Command line tools will need to make guesses at times if the asset doesn’t conform to expected guidelines and can result in assets that don’t render as intended. Keeping control over the export gives you more power to create assets that look exactly the way you want them to.

# Texture Requirements

The glTF format supports the following textures for the Metallic-Roughness PBR model:

- Base Color
- Metallic
- Roughness
- Normal
- Ambient Occlusion
- Emission

The format does expect the textures in a specific format, however. The **Base Color**, **Normal**, and **Emissi**on textures are saved as individual files, preferably a PNG as the format is lossless. The **Ambient Occlusion**, **Roughness**, and **Metallic** textures are saved in a single channel-packed texture to reduce the number of texture loads. The textures need to be packed into the channels of your texture as follows:

- Red: **Ambient Occlusion**
- Green: **Roughness**
- Blue: **Metallic**

Going forward, I will refer to this channel-packed texture as the ORM texture for **O**cclusion, **R**oughness, and **M**etallic.
