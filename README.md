# Akuma's DNA+

Custom DNA replacements for **Crusader Kings III: A Game of Thrones**.

## Adding a New DNA

Each new character requires three things:

1. **DNA data**
2. **Dummy character**
3. **Replacement entry**

All custom IDs created for Akuma's DNA+ must use the `akumas_` prefix.

---

## 1. Add the DNA

Open:

`common/dna_data/akumas_dna_data.txt`

Add the DNA exported from the CK3 Portrait Editor.

```txt
akumas_rhaegar_targaryen = {
    portrait_info = {
        genes = {
            # DNA goes here
        }
    }

    enabled = yes
}
```

Use a clear ID following this format:

`akumas_character_name`

Examples:

```txt
akumas_rhaegar_targaryen
akumas_daenerys_targaryen
akumas_jon_snow
akumas_arya_stark
```

---

## 2. Add the Dummy Character

Open:

`history/characters/akumas_dna_dummies.txt`

Create a dummy character using the same ID as the DNA:

```txt
akumas_rhaegar_targaryen = {
    name = "Rhaegar"
    dynasty = none
    religion = valyrian_faith
    culture = high_valyrian
    dna = akumas_rhaegar_targaryen

    8000.1.1 = {
        birth = yes
    }
}
```

The important line is:

```txt
dna = akumas_rhaegar_targaryen
```

The DNA ID and dummy character ID should match:

```txt
DNA:   akumas_rhaegar_targaryen
Dummy: akumas_rhaegar_targaryen
```

The dummy character only stores the custom appearance. It is not intended to appear during normal gameplay.

---

## 3. Add the Replacement

Open:

`common/scripted_effects/akumas_dna_effects.txt`

Add the original AGOT character and point it to our dummy:

```txt
character:Targaryen_3 ?= {
    copy_inheritable_appearance_from = character:akumas_rhaegar_targaryen
}
```

In this example, `Targaryen_3` is the original AGOT character ID and `akumas_rhaegar_targaryen` is our dummy character.

The original AGOT character ID must **not** be renamed.

### Correct

```txt
character:Targaryen_3 ?= {
    copy_inheritable_appearance_from = character:akumas_rhaegar_targaryen
}
```

### Incorrect

```txt
character:akumas_Targaryen_3 ?= {
    copy_inheritable_appearance_from = character:akumas_rhaegar_targaryen
}
```

Only IDs created by us use the `akumas_` prefix.

---

## Complete Example

If the original AGOT character ID is:

`Targaryen_3`

### DNA

Add to `common/dna_data/akumas_dna_data.txt`:

```txt
akumas_rhaegar_targaryen = {
    portrait_info = {
        genes = {
            # DNA goes here
        }
    }

    enabled = yes
}
```

### Dummy

Add to `history/characters/akumas_dna_dummies.txt`:

```txt
akumas_rhaegar_targaryen = {
    name = "Rhaegar"
    dynasty = none
    religion = valyrian_faith
    culture = high_valyrian
    dna = akumas_rhaegar_targaryen

    8000.1.1 = {
        birth = yes
    }
}
```

### Replacement

Add to `common/scripted_effects/akumas_dna_effects.txt`:

```txt
character:Targaryen_3 ?= {
    copy_inheritable_appearance_from = character:akumas_rhaegar_targaryen
}
```

The replacement works like this:

```txt
DNA
akumas_rhaegar_targaryen
        ↓
Dummy Character
akumas_rhaegar_targaryen
        ↓
Original AGOT Character
Targaryen_3
        ↓
Custom appearance is applied
```

---

## Adding Multiple Characters

Repeat the same process for every new character:

```txt
character:Targaryen_3 ?= {
    copy_inheritable_appearance_from = character:akumas_rhaegar_targaryen
}

character:Targaryen_4 ?= {
    copy_inheritable_appearance_from = character:akumas_daenerys_targaryen
}

character:Stark_1 ?= {
    copy_inheritable_appearance_from = character:akumas_jon_snow
}
```

Each replacement must have a corresponding DNA and dummy character.

---

## Naming Rules

Everything created specifically for Akuma's DNA+ must use the `akumas_` prefix.

Recommended:

```txt
akumas_rhaegar_targaryen
akumas_daemon_targaryen
akumas_arya_stark
akumas_jaime_lannister
```

Avoid generic names:

```txt
dna_1
new_dna
dummy_01
character_test
```

Original CK3 and AGOT IDs must remain unchanged when referenced.

---

## Checklist

Before committing a new character:

- [ ] DNA added to `akumas_dna_data.txt`
- [ ] DNA ID starts with `akumas_`
- [ ] Dummy added to `akumas_dna_dummies.txt`
- [ ] Dummy ID starts with `akumas_`
- [ ] Dummy points to the correct DNA
- [ ] Correct original AGOT character ID used
- [ ] Replacement added to `akumas_dna_effects.txt`
- [ ] Original AGOT IDs remain unchanged

Once these entries are added, the existing Akuma's DNA+ framework handles the appearance replacement automatically.
