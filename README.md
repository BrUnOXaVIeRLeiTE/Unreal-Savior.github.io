[![Savior](https://i.imgur.com/fj3ZcYM.png)](https://www.unrealengine.com/marketplace/en-US/product/savior)



# Savior Plugin Documentation

 Savior is a C++ tool designed to extend Unreal's save system, providing a more powerful serialization
 framework for complex Unreal projects.
 Savior is a custom serialization system built from scratch with
 efficiency in mind, together with a focus in productivity and ease-of-use in Unreal.
 This documentation summarizes most common doubts of new users, most common mistakes, and the best solutions to achieve developer's goals.


># Features

| Productivity |
| ------------ |
| Savior eliminates micro-management of individual properties, becoming a valuable time saver for small teams.      |
| Marking a property with Unreal's 'Save Game' exposes property to the save system, no mirror property required.    |
| A rich library of helper functions brings free customization of the save process within blueprints, no coding.    |
| Deleting or adding new blueprint properties will not corrupt existing save files; Contrary to other save systems. |
| Built-in versioning system helps patching live games, without causing players to lose existing progress.          |

| Performance |
| ----------- |
| Savior abuses Unreal's multi-threading capabilities. Saving data is absurdly fast, only limited by target hardware. |
| Blueprint properties are read directly from target, mirror property in slots not required, increasing performance.  |
| Actor's location, rotation, scale, velocity, mesh, materials; Are all recorded from multi-threaded algorithms.      |

| Utility |
| ------- |
| Savior is based on *slots* to persist data. |
| A full HUD system ships with the plugin, making easy to implement loading screens, slot selection screens.        |
| Data loading progress is automatically calculated, generating feedback progress bars without developer efforts.   |

---

># Contents

[Installation](#installation)<br>
[How to Setup a Slot](#how-to-setup-a-slot)<br>
[How to Save & Load](#how-to-save-load)<br>
[How to Setup Pickups](#how-to-setup-pickups)<br>
[How to Setup Procedural Actors](#how-to-setup-procedural-actors)<br>
[Understanding SGUID](#understanding-sguid)<br>
[Tips & Tricks](#tips-n-tricks)<br>
[Savior in C++](#savior-in-c)<br>
[FAQ](#faqs)<br>
[Extras](#extras)<br>
[Technical Specifications](#technical-specifications)<br>

---

># Savior API

### Slot Methods:

* [Synchronous Slot Methods](https://brunoxavierleite.github.io/Savior2API.github.io/Savior3/Savior3.html)


### Asynchronous Methods:

* [Load Game Instance (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameInstance/nodes/UK2Node_AsyncAction.html)
* [Load Game Instance [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameInstance_Callback/nodes/UK2Node_AsyncAction.html)
* [Load Game Mode (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameMode/nodes/UK2Node_AsyncAction.html)
* [Load Game Mode [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameMode_Callback/nodes/UK2Node_AsyncAction.html)
* [Load Game World (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameWorld/nodes/UK2Node_AsyncAction.html)
* [Load Game World [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameWorld_Callback/nodes/UK2Node_AsyncAction.html)
* [Load Level (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadLevel/nodes/UK2Node_AsyncAction.html)
* [Load Level [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadLevel_Callback/nodes/UK2Node_AsyncAction.html)
* [Open Level (+HUD)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_OpenLevel/nodes/UK2Node_AsyncAction.html)
* [Open Level (+HUD) [+Callback]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_OpenLevel_Callback/nodes/UK2Node_AsyncAction.html)
* [Save Game Instance (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameInstance/nodes/UK2Node_AsyncAction.html)
* [Save Game Instance [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameInstance_Callback/nodes/UK2Node_AsyncAction.html)
* [Save Game Mode (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameMode/nodes/UK2Node_AsyncAction.html)
* [Save Game Mode [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameMode_Callback/nodes/UK2Node_AsyncAction.html)
* [Save Game World (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameWorld/nodes/UK2Node_AsyncAction.html)
* [Save Game World [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameMode_Callback/nodes/UK2Node_AsyncAction.html)
* [Save Level (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveLevel/nodes/UK2Node_AsyncAction.html)
* [Save Level [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveLevel_Callback/nodes/UK2Node_AsyncAction.html)


### Serializable Interface:

* [Event: On Loaded](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnLoaded.html)
* [Event: On Marked (Auto-Destroy)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnMarkedAutoDestroy.html)
* [Event: On Prepare To Load](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnPrepareToLoad.html)
* [Event: On Prepare To Save](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnPrepareToSave.html)
* [Event: On Saved](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnSaved.html)

### Procedural Interface:

* [Event: On Begin Respawn](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Procedural/nodes/OnBeginRespawn.html)
* [Event: On Finish Respawn](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Procedural/nodes/OnFinishRespawn.html)

### HUD Custom Class:

* [Event: On Begin Load-Screen](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/OnBeganLoadScreen.html)
* [Event: On Finish Load-Screen](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/OnFinishedLoadScreen.html)
* [Invoke Load Screen (Blur)](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/DisplayBlurLoadScreenHUD.html)
* [Invoke Load Screen (Splash)](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/DisplaySplashLoadScreenHUD.html)
* [Remove Load Screen](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/RemoveLoadScreen.html)
* [Hide Slots UI](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/HideSlotPickerHUD.html)
* [Show Slots UI](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/ShowSlotPickerHUD.html)

---

># Quick Guides


## Installation

Open the Epic Games Launcher and install the Savior plugin from Marketplace, or the FAB store.
You must have a valid Epic games account to purchase any products from Unreal Marketplace.


## How to Setup a Slot

As always, create a Slot Asset on Asset Browser;
Opening the Asset you can quickly adjust default Properties such as Default Player Name, Levels Thumbnails, etc:

![1](https://d3kjluh73b9h9o.cloudfront.net/original/4X/c/3/b/c3bdef167fa243f8d9973e63414f0fcc6db64841.png)

![2](https://d3kjluh73b9h9o.cloudfront.net/original/4X/a/4/6/a46bca0c4a52deb7d0c9aef426f9a2567276e5f8.png)


## How to Save Load

All you have to do is right click any graph on any of your Blueprints and search from one of main nodes in “Savior” section.
These main Save/Load functions automatically creates a runtime instance of a Slot object for you… So you don’t have to instantiate anything, just reference the Slot Asset and let the node work:

![3](https://www.dropbox.com/scl/fi/vcilziv5twrbdtskhodlf/muiPiDr.png?rlkey=0u3zmj2qdh85z2ex16eadeaek&st=ozhr2hpa&raw=1)

From any UMG Widget you simply setup your “On Button Clicked” events to call one of these “Savior 2” functions.
It’s THAT simple, everything in scope marked ‘SaveGame’ tag will save or load:

![4](https://www.dropbox.com/scl/fi/f626drojkgvpixl1b7fyh/JNseaSb.png?rlkey=q6zwd4ygfw6ajo1i4tg48ucf2&st=bn1kw688&raw=1)


### Manual Slot Instances Management

If you desire to perform custom Save/Load operations and not necessarily just fire a "**Save Game World**" to save everything, you can do so by building a process starting from the **New Slot Instance Node**. Example:

![SS1](https://d3kjluh73b9h9o.cloudfront.net/optimized/4X/6/c/8/6c852f147dcf77871ce3ea3c4d9b44297fa101e8_2_1035x442.png)
![SS2](https://d3kjluh73b9h9o.cloudfront.net/optimized/4X/2/a/e/2ae8e6580ad262018e0b0b16a8893671fafa40b9_2_1035x379.png)

---

## How to Setup Pickups

Any Actor you wish to remember it was destroyed and should not respawn on Level load, you have to add a “Destroyed” Boolean Property to it. And mark it ‘Save Game’ tag as well:

![5](https://www.dropbox.com/scl/fi/p41s7y97gcpdosbfqayt9/Rmq7TDb.png?rlkey=tgj1oi319qctezk5hijwkiycw&st=y2j7csm5&raw=1)

The Property must be a Boolean named “Destroyed”, case sensitive.
The Property must be marked ‘Save Game’ tag.

Then in your Blueprint Graph, create a new Function calling it whatever you’d like, this Function will be a substitute of “Destroy Actor” node for the Game.
Inside this Graph Function set the value of “Destroyed” to true, but don’t destroy this Actor before you save the Game, maybe hide it instead:

![6](https://www.dropbox.com/scl/fi/hafhp8796np8mg9tfxkw5/KHPG44O.png?rlkey=ctps0d6df2vda4yi6jplopfzr&st=5wp0vcel&raw=1)

Having that Boolean “Destroyed” Property set to TRUE will tell the Plugin that this Actor must destroy itself once the Level was loaded, making it be gone the next time a Player visits that Level…

To do that, when you want a Pickup to be destroyed, simply call your newly created Function that hides the Actor and sets “**Destroyed**” to True instead of destroying the Actor with a Destroy node:

![7](https://www.dropbox.com/scl/fi/hsie31jw9wzj7jrzldsmy/uvp1CJM.png?rlkey=x897kl5jopbu0oeznfk1q7cop&st=vpm0gwkf&raw=1)

Once the Game is saved, the Plugin will Destroy the Actor after it’s “Destroyed” Property has been recorded, so the Actor won’t be left there consuming memory.

> ![!](https://www.dropbox.com/scl/fi/xlh9eu8vyiunaod4mkj0l/warning.png?rlkey=fqe2nvvt8jxenrkp1p44koghn&raw=1)  **WARNING:**
> If you overwrite the data existing in a slot file, the 'Destroyed' record will be erased as well. So, if your design involves persistently destroyed enties, you most likely want to **LOAD** a slot from file before saving again! This way your destroyed actors records will never be erased whenever your slot files are updated with new data.

---

## How to Setup Procedural Actors

An Actor, or Component, you are spawning at Runtime will be saved as usual.
However loading them back is a complex task because we cannot control whatever ID the internal engine will assign to a runtime spawned Object.
Often the new Object’s ID will be random internal pointer that used to reference another object; to overcome this obstacle to Save & Load “Procedural Actor” properly, your Procedural Class is required to implement three things:

Implement the “**SAVIOR_Procedural**” Function Interface.
Include a “Guid” Property to its Variables List, named “**SGUID**”.
In its Construction Script, call a special node called “Make SGUID”.
Those three simple steps above will guarantee your Procedural Class will be loaded correctly from Slot’s Data without mismatching Data with another instance of your Class also spawned in Runtime, turning them into Absolutely Identifiable Procedural Objects.

![8](https://d3kjluh73b9h9o.cloudfront.net/original/4X/2/1/5/21584394bbe199b039f41454671d655f75e40c8e.png)

First, within desired Procedural Actor’s Blueprint, we have to implement our “Procedural” Function Interface:

![9](https://d3kjluh73b9h9o.cloudfront.net/original/4X/c/0/a/c0acb82e6d13bba0ee6a8ef9250b9f434ebaf730.png)

Once that is done, we now have to create a “Guid” Property for the Procedural Class and name it “SGUID”:

![10](https://d3kjluh73b9h9o.cloudfront.net/original/4X/0/f/0/0f03fd2124f7673c272f96de806281b6687985e7.png)

The Property must be a Guid Struct named “SGUID”. Savior will ‘read’ the Property and expects it to be this type, otherwise it will be ignored.
The Property must be marked ‘Save Game’ tag to be visible to the Auto-Save System.

That been done, only step left now is making sure SGUID’s value is persistent and unique.
That would be a headache for you to do, so instead of trying to control its behavior, there’s a node that can do that for you within a Construction Script…

Add the “Make SGUID” node to your Construction Script Graph and assign its output value to the “SGUID” Property:

![11](https://d3kjluh73b9h9o.cloudfront.net/optimized/4X/3/9/d/39d3efaef5aea2a57023b5ba3573176fbfc94af2_2_1035x585.png)

Do NOT use a default “New Guid” node! The Guids created by that aren’t persistent, it would break our logic.

And it’s done, your ‘Procedural Class’ is ready to be freely spawned in Runtime and be automatically respawned with it’s correct Property’s values restored once the Game is reloaded from a Slot.

## Understanding SGUID

There are three types of Actors in any Unreal Engine world:
* Actors you've placed in the Level by hand.
* Actors that are unique, but only exist at runtime.
* Actors that you spawn multiple instances of same class at runtime.

For each type of Actor above, you have to understand how Unreal Engine identifies these instances. When you place any amount of instantiated Actors in the Level, Unreal Editor automatically resolves instance ID, these IDs created are the same at runtime.<br>
When you have a Game Mode that is spawned at runtime, and then spawns an instance of a Character, new IDs are created, but you usually treat these Actors as singleton Actors. That means, if Savior knows the class of your Game Mode, it doesn't have to care if that Character is Character_C_0 or Character_C_55.<br>
It knows that it's the Player's Character. However when you spawn at runtime any amount of instances of any arbitrary class, the same process of resolving instance IDs is performed by the engine; and Savior cannot assume it knows which Actor is which, because every time the application launches, different IDs will be applied.
<br>
<br>
So, in order to identify Actors properly, Savior requires a SGUID property in the base class of the Actors you are spawning. Example of a SGUID value, a property of type Guid (or FGuid in C++):

> 1D371B88-46704C84-75D4E493-62CCF89A

Savior uses these structs, a composition of various integer values, to properly identify Actor instances, regardless of instance ID these Actors were given by the engine. Because Unreal Engine by default applies ID shuffling to Actors when you package a Shipping Build, having a SGUID value is very important for Savior to be sure it knows who is who when saving and loading data.

So, you have very simple choices to deal with this...

1. Create a value for your **SGUID** property manually, taking pen note of who is who in your Level.
2. Use [Create Once Node](https://www.dropbox.com/scl/fi/z40hzh7f9dzbf5ibb4svn/P1pnhSy.png?rlkey=g2phuumxh065bysrp7v34gvn5&st=94yum1zb&raw=1) for Actors you keep in a list.
3. Use [Make SGUID Node](https://www.dropbox.com/scl/fi/sb8it2stkxfzw9zmrxk0v/C02pdNZ.png?rlkey=oq5xafjg50phui5dtkuokf27u&st=wcljgs51&raw=1) for Actors you spawn at runtime, but expect them to act as a Singleton entity.

Example:

This Player Character is spawned at runtime... Here its ID has a suffix " _C_0 ", but that can be changed by the engine.

![12](https://camo.githubusercontent.com/dfed70559965fcceb4ab61141ddc1301f929cafea91d7b4d27f83c2f9d973ec7/68747470733a2f2f692e696d6775722e636f6d2f787866617150642e706e67)

So, to counter this inconvenience, I add to Blueprint a SGUID property and use in its Construction Script a Make SGUID node.

![13](https://camo.githubusercontent.com/2b398cae80fdfee452d66d55024f597492b61073bef8f82ee7044030a7a88c69/68747470733a2f2f692e696d6775722e636f6d2f43303270644e5a2e706e67)

#### ![!](https://www.dropbox.com/scl/fi/xlh9eu8vyiunaod4mkj0l/warning.png?rlkey=fqe2nvvt8jxenrkp1p44koghn&raw=1)  **IMPORTANT:**
> Since Fortnite cheaters appeared, Epic Games is encrypting ID of some core actors, like the main playable character. But they only do this at runtime (shipping package), this is hardcoded into the Unreal Engine.

> You won’t notice that until you package for shipping. In shipping mode Epic seem to add memory address encoded into the internal name of the actor… and that is going to change every time you launch the game (to difficult the work of memory scanners used by cheaters).

> So, for a main character, I simply will NOT use the SGUID making nodes in constructor…

> I just leave it as a **0000-0000-0000** guid instead.

---

## Tips n Tricks

#### ![!](https://www.dropbox.com/scl/fi/my4qzni9n6boti7m7cziu/bulb.png?rlkey=vxkudaeww096qjj8lz1yxsvu4&st=9umm2gpx&raw=1) One Template Class for multiple slot instances
* You only need 1 slot template asset, then you can just override the ***Slot File Name*** property, like in this example below:

![14](https://d3kjluh73b9h9o.cloudfront.net/original/4X/1/f/e/1fe095bc972d78fec11609e2db0b805e25a17067.png)

---

## Savior in C++

If you have native C++ classes you desire to implement Savior's API directly, follow these steps:

#### Build.cs:
You must add Savior3 module to your Build.cs list of dependencies >>
```c++
PublicDependencyModuleNames.AddRange(new string[]
{
    "Core", "CoreUObject", "Engine", "InputCore", "Savior"
});
```

#### C++:
Your class definition have to include Savior hears >>
```c++
#include "Savior.h"
#include "SaviorMetaData.h"
```

Your class should implement one or both of Savior's event interfaces >>
```c++
UCLASS()
class MYGAME_API ALoot : public AActor, public ISAVIOR_Serializable, public ISAVIOR_Procedural
{
    // ...
}
```

Override Interface functions >>
```c++
UFUNCTION() virtual void OnLoaded_Implementation(const FSlotMeta &MetaData) override;
```

Include and construct SGUID Property >>
```c++
UPROPERTY() FGuid SGUID;
```
```c++
AMyActor::AMyActor()
{
    SGUID = USavior3::MakeActorGUID( this , EGuidGeneratorMode::ResolvedNameToGUID );
}
```

#### Full Example:

># .H
```c++
#pragma once

#include "Savior3.h"
#include "SaviorMetaData.h"
#include "CoreMinimal.h"
#include "GameFramework/Actor.h"
#include "Loot.generated.h"

UCLASS()
class MYGAME_API ALoot : public AActor, public ISAVIOR_Serializable, public ISAVIOR_Procedural
{
    GENERATED_BODY()
    
public:	
    // Sets default values for this actor's properties
    ALoot();

    UPROPERTY(EditDefaultsOnly, Category = Mesh)
        class USkeletalMeshComponent* Mesh;
    UPROPERTY(EditDefaultsOnly, Category = Mesh)
        class USkeletalMeshComponent* Outline;

    /** Returns MeshSK subobject **/
    UFUNCTION(BlueprintCallable)
        class USkeletalMeshComponent* GetSKMesh() const { return Mesh; }

    //image to display in Inventory
    UPROPERTY(EditAnywhere, Category = "Inventory")
        class UTexture* InventoryImage;
    
    UPROPERTY(EditAnywhere, Category = "Inventory")
        FName ItemName;
    UFUNCTION(BlueprintCallable)
        class UTexture* GetImage() { if (InventoryImage != nullptr) return InventoryImage; else return nullptr; }
    UFUNCTION(BlueprintCallable)
        FName GetItemName() { return ItemName; }

    UFUNCTION(BlueprintCallable)
        void DecrementAmnt() { --Amnt; }

    class UMaterialInstanceDynamic* MatOutline;
    class UMaterialInstanceDynamic* MatMesh;
protected:
    // Called when the game starts or when spawned
    virtual void BeginPlay() override;

public:	
    // Called every frame
    virtual void Tick(float DeltaTime) override;

    UFUNCTION(BlueprintCallable)
        virtual void BeginView();
    UFUNCTION(BlueprintCallable)
        void EndView();

    virtual void Equip();
    virtual void UnEquip();

    UFUNCTION()
        void PickedUp();
    UFUNCTION()
        void Dropped(FVector DropLoc);

    UFUNCTION(BlueprintImplementableEvent)
        void DroppedBP();


    //For Inventory/UI purposes. Determines where in inventory and how much space each takes up.
    UPROPERTY(EditAnywhere)
        int32 XPos;
    UPROPERTY(EditAnywhere)
        int32 YPos;
    UPROPERTY(BlueprintReadWrite, Category = "Inventory")
        int32 XFill;
    UPROPERTY(BlueprintReadWrite, Category = "Inventory")
        int32 YFill;
    UPROPERTY(EditAnywhere)
        int32 Rarity;

    //for loading
    UPROPERTY(SaveGame)
        FGuid SGUID;
    UPROPERTY(EditAnywhere, SaveGame)
        bool bIsOwned = false;
    UPROPERTY(EditAnywhere, SaveGame)
        int32 HotBarIndex = 5; //0-4 index, 5 is not on hotbaar
    UPROPERTY(EditAnywhere, SaveGame)
        bool bIsEquipped = false; 
    UPROPERTY(EditAnywhere, SaveGame)
        FIntPoint SavedPosition;
    UFUNCTION()
        virtual void OnLoaded_Implementation(const FSlotMeta &MetaData) override;

    //logic for stackable items such as arrows/bombs/healing item
    UPROPERTY(BlueprintReadWrite)
        bool bIsStackable = false;
    UPROPERTY(BlueprintReadOnly)
        int32 Amnt = 1;

private:

    float OutlineScale = .5f;

};
```

># .CPP
```c++
#include "Loot.h"
#include "Engine/Texture.h"
#include "Materials/MaterialInstanceDynamic.h"
#include "Materials/MaterialInterface.h"
#include "Components/SkeletalMeshComponent.h"

// Sets default values
ALoot::ALoot()
{
    // Set this actor to call Tick() every frame.  You can turn this off to improve performance if you don't need it.
    PrimaryActorTick.bCanEverTick = true;

    SGUID = USavior3::MakeActorGUID(this,EGuidGeneratorMode::ResolvedNameToGUID);

    Mesh = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("Mesh"));
    Mesh->SetCollisionEnabled(ECollisionEnabled::QueryAndPhysics);
    Mesh->SetCollisionResponseToAllChannels(ECollisionResponse::ECR_Block);
    Mesh->SetCollisionResponseToChannel(ECollisionChannel::ECC_Pawn, ECollisionResponse::ECR_Ignore);
    Mesh->SetSimulatePhysics(false);

    SetRootComponent(Mesh);

    Outline = CreateDefaultSubobject<USkeletalMeshComponent>(TEXT("Outline"));
    Outline->SetCollisionEnabled(ECollisionEnabled::NoCollision);
    Outline->SetupAttachment(Mesh, FName("None"));

    InventoryImage = CreateDefaultSubobject<UTexture>(TEXT("Inventory Image")); 
}

// Called when the game starts or when spawned
void ALoot::BeginPlay()
{
    Super::BeginPlay();
    Outline->SetMasterPoseComponent(Mesh);	
    
    MatOutline = UMaterialInstanceDynamic::Create(Outline->GetMaterial(0), this);
    MatMesh = UMaterialInstanceDynamic::Create(Mesh->GetMaterial(0), this);
    Outline->SetMaterial(0, MatOutline);
    Mesh->SetMaterial(0, MatMesh);

    EndView();
}

// Called every frame
void ALoot::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);

}

void ALoot::BeginView()
{
    MatOutline->SetScalarParameterValue(FName("Glow"), 500.0f);
    MatOutline->SetScalarParameterValue(FName("MaskAmnt"), 1.0f);
    if (Rarity == 1) MatOutline->SetVectorParameterValue(FName("Color"), FColor::Green);
    if (Rarity == 2) MatOutline->SetVectorParameterValue(FName("Color"), FColor::Blue);
    if (Rarity == 3) MatOutline->SetVectorParameterValue(FName("Color"), FColor::Purple);
    if (Rarity == 4) MatOutline->SetVectorParameterValue(FName("Color"), FColor::Red);	
    if (Rarity == 5) MatOutline->SetVectorParameterValue(FName("Color"), FColor::Yellow); 
}

void ALoot::EndView()
{
    MatOutline->SetScalarParameterValue(FName("Glow"), 0.0f);
    MatOutline->SetScalarParameterValue(FName("MaskAmnt"), 0.0f);
}

void ALoot::Equip()
{
    bIsEquipped = true;
    MatMesh->SetScalarParameterValue(FName("OffsetFOV"), 1.0f);
}

void ALoot::UnEquip()
{
    bIsEquipped = false;
}

void ALoot::PickedUp()
{
    bIsOwned = true;
    Mesh->SetSimulatePhysics(false);
    Mesh->SetCollisionEnabled(ECollisionEnabled::NoCollision);
    Mesh->SetCollisionResponseToAllChannels(ECollisionResponse::ECR_Overlap);
    Mesh->SetCastShadow(false);
}

void ALoot::Dropped(FVector DropLoc)
{
    bIsOwned = false;
    MatMesh->SetScalarParameterValue(FName("OffsetFOV"), 0.0f);
    Mesh->SetSimulatePhysics(true);
    Mesh->SetCollisionEnabled(ECollisionEnabled::QueryAndPhysics);
    Mesh->SetCollisionResponseToAllChannels(ECollisionResponse::ECR_Block);
    Mesh->SetCollisionResponseToChannel(ECollisionChannel::ECC_Pawn, ECollisionResponse::ECR_Ignore);
    Mesh->SetCastShadow(true);
    EndView();
    SetActorLocation(DropLoc, true, nullptr, ETeleportType::TeleportPhysics); 

    DroppedBP();
}

void ALoot::OnLoaded_Implementation(const FSlotMeta &MetaData)
{
    //GetCharacterNameRenderer()->SetText(CharacterName);

    LOG_SV(true, ESeverity::Warning,
        FString::Printf(TEXT("OnLoaded()  ==>>  %s  ::  %s"),
            *MetaData.SaveLocation,
            *GetName()
        )
    );

    if ( bIsOwned ) {
        auto Player = GetWorld()->GetFirstPlayerController();
        if (!Player) return;

        // call event...
    }
}
```

---

## FAQs

> How, why my Actor isn't saving?

 Chances are you did not setup a SGUID Property properly.

> Save World or Game Mode returns Failed result, why?

 Check thread state with Get Thread Safety node. If you have another save process running, you have to wait until previous process is complete to start a new one.

> I still can't save anything?!
 Make sure you are creating an instance with **New Slot Instance node**. Don't try to save data directly into your
 Slot Class.

---

## Extras

![!](https://www.dropbox.com/scl/fi/my4qzni9n6boti7m7cziu/bulb.png?rlkey=vxkudaeww096qjj8lz1yxsvu4&st=9umm2gpx&raw=1) Savior is one of few save systems in Unreal that supports saving object pointers. And it's the only that actually supports saving a chain of nested UObjects. This is perfect for complex [inventory systems based on the UObject](https://github.com/BrUnOXaVIeRLeiTE/UESimpleInventory#) class.

![!](https://www.dropbox.com/scl/fi/my4qzni9n6boti7m7cziu/bulb.png?rlkey=vxkudaeww096qjj8lz1yxsvu4&st=9umm2gpx&raw=1) In Unreal Engine 5, Savior has built-in support for recording and restoring states of [Chaos Destruction System](https://dev.epicgames.com/documentation/en-us/unreal-engine/chaos-destruction-in-unreal-engine)'s fracturing and geometry collections (*EXPERIMENTAL*).

![!](https://www.dropbox.com/scl/fi/my4qzni9n6boti7m7cziu/bulb.png?rlkey=vxkudaeww096qjj8lz1yxsvu4&st=9umm2gpx&raw=1) In Unreal Engine 5, Savior has partial built-in support for saving and loading the state of [Mutable Characters](https://dev.epicgames.com/community/learning/tutorials/yjw9/unreal-engine-mutable-tutorials) and their parts (*EXPERIMENTAL*).

---

## Module Specifications

---
# Savior Core – C++ API

The following is technical documentation for the `Savior.h` header file from the Unreal Engine plugin **Savior Auto-Save Plugin** by Bruno Xavier Leite.

---

## 📦 USaviorSettings – Plugin Configuration Settings

This class holds plugin-level configuration data, categorized under gameplay, performance, and object handling.

### 🧩 UPROPERTY Members

#### General Settings
- **`int32 DefaultPlayerID`**: ID for the default player controller.
- **`int32 DefaultPlayerLevel`**: Local player's level (for progression-based games).
- **`FString DefaultPlayerName`**: Name or alias of the player.
- **`FString DefaultChapter`**: Current chapter of the game/story.
- **`FString DefaultLocation`**: Name of the map or level being saved.

#### Performance
- **`bool RespawnDynamicActors`**: Enable auto-respawn of missing actors.
- **`bool RespawnDynamicComponents`**: Enable auto-respawn of missing components.
- **`bool AccurateDynamicRespawnChecks`**: Ensures accurate respawn, potentially impacting performance.

#### Reflector Scope
- **`TSet<TSubclassOf<UObject>> InstanceScope`**: Auto-instantiation classes.
- **`TSet<TSubclassOf<UObject>> RespawnScope`**: Auto-respawn target classes.

---

## 💾 USavior – Core Save/Load Slot Object

This class provides a runtime object that handles saving and loading of game state data.

### 🧩 UPROPERTY Members

#### Configuration
- `Debug`, `DeepLogs`, `RuntimeMode` – Control debug output and threading behavior.
- `ObjectScope`, `ComponentScope`, `ActorScope` – Define serialization targets.

#### Load Screen
- Includes customizable fields like `LoadScreenMode`, `SplashImage`, `FeedbackSAVE`, `BackBlurPower`, etc.

#### UI/UX
- `SlotFileName`, `SlotThumbnail`, `LevelThumbnails` – Control UI visuals and file metadata.

#### Events
- Bindable multicast delegates such as `EVENT_OnBeginDataSAVE`, `EVENT_OnFinishDataLOAD`, etc.

#### Misc
- Runtime-related fields: `WriteMetaOnSave`, `IgnorePawnTransformOnLoad`, `SlotMeta`, `SlotData`, `World`

---

## 🛠️ UFUNCTION Methods Overview

### 1. Core Slot File I/O
- `WriteSlotToFile`, `ReadSlotFromFile`, `DeleteSlotFile`, `FindSlotFile`
- `SaveSlotMetaData`, `LoadSlotMetaData`
- `GetSlotMetaData()`

### 2. Object/Component/Actor Save/Load
- Save: `SaveObject`, `SaveActor`, `SaveComponent`, etc.
- Load: `LoadObject`, `LoadActor`, `LoadComponent`, etc.
- Hierarchical: `SaveObjectHierarchy`, `LoadActorHierarchy`, etc.

### 3. Game Scope Save/Load
- `SaveGameWorld`, `LoadGameWorld`
- `SaveGameMode`, `LoadGameMode`
- `SaveGameInstance`, `LoadGameInstance`
- `SavePlayerState`, `LoadPlayerState`

### 4. Level and Data Layer Serialization
- `SaveLevel`, `LoadLevel`
- `SaveWorldLayers`, `LoadWorldLayers`
- `SaveGameFeatures`, `LoadGameFeatures`

### 5. Low-Level Record Management
- `GenerateRecord_*`, `UnpackRecord_*`
- `FindRecordByName`, `FindRecordByGUID`
- `AppendDataRecords`, `InsertDataRecord`, `RemoveDataRecordByName`, etc.

### 6. GUID and ID Utilities
- `MakeObjectGUID`, `CreateSGUID`, `MatchesGUID`, `MarkActorAutoDestroyed`, etc.
- Check/Generate/Query SGUIDs

### 7. UI/UX Getters and Setters
- `SetChapter`, `SetProgress`, `SetPlayerName`, `GetSaveTimeISO`, etc.

### 8. Utility + Meta Methods
- `NewSlotInstance`, `GetClassDefaultObject`, `ShadowCopySlot`
- `GetSaveProgress`, `GetLoadWorkload`, etc.

---

## ✅ Summary

The `USavior` class exposes a highly granular and flexible API to Unreal Engine’s Blueprint system, empowering developers to implement robust save/load functionality, auto-respawn logic, UI/UX enhancements, and system configuration—entirely through C++ or Blueprints.
