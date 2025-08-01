# RPG Adventure Scenarios

This directory contains pre-configured parameter sets for different adventure themes and styles. Each scenario has been crafted to showcase different aspects of the adventure engine and provide varied gameplay experiences.

## Available Scenarios

### 1. **cyberpunk-neural-heist.yml**
**Theme:** Cyberpunk  
**Length:** 10 events (Medium)  
**Party Size:** 4 characters  
**Complexity:** High-stakes, fast-paced  

A daring heist to steal experimental neural implants from a megacorporation's secure facility. Features hacking, corporate espionage, and augmented reality combat. The team must navigate both physical security and digital countermeasures while dealing with potential betrayals and moral dilemmas about transhumanism.

**Best For:** Players who enjoy heist mechanics, technology-focused challenges, and morally gray decisions.

---

### 2. **scifi-first-contact.yml**
**Theme:** Sci-Fi  
**Length:** 15 events (Long)  
**Party Size:** 5 characters  
**Complexity:** Balanced with diplomatic focus  

Humanity's first encounter with an alien species goes catastrophically wrong when a translation error sparks an interstellar incident. The crew must navigate cultural misunderstandings, prevent war, and uncover a conspiracy that threatens both civilizations.

**Best For:** Players who enjoy diplomacy, exploration, and complex problem-solving over combat.

---

### 3. **mystery-mansion-murders.yml**
**Theme:** Mystery  
**Length:** 8 events (Short)  
**Party Size:** 3 characters  
**Complexity:** Investigation-heavy  

A weekend gathering at an isolated mansion turns deadly when the host is found murdered. As a storm traps everyone inside, more deaths follow a cryptic pattern. The investigators must identify the killer before they become the next victims.

**Best For:** Players who enjoy deduction, social intrigue, and atmospheric tension.

---

### 4. **postapoc-water-wars.yml**
**Theme:** Post-Apocalyptic  
**Length:** 12 events (Medium)  
**Party Size:** 4 characters  
**Complexity:** Survival-focused  

In the wasteland, water is more valuable than gold. When the party discovers a map to a legendary water purification facility, they must race against rival gangs, navigate irradiated zones, and decide whether to keep the water for themselves or share it with struggling settlements.

**Best For:** Players who enjoy resource management, moral choices, and gritty survival scenarios.

---

### 5. **superhero-reality-crisis.yml**
**Theme:** Superhero  
**Length:** 14 events (Long)  
**Party Size:** 6 characters  
**Complexity:** Epic scale  

When reality begins fracturing across the multiverse, a team of heroes from different dimensions must work together despite conflicting methods and philosophies. They face corrupted versions of themselves while trying to prevent the complete collapse of all realities.

**Best For:** Players who enjoy epic battles, character drama, and reality-bending challenges.

---

### 6. **fantasy-awakened-peasant.yml**
**Theme:** Fantasy  
**Length:** 9 events (Short)  
**Party Size:** 3 characters  
**Complexity:** Intense, escalating stakes  

A humble farmer's life is shattered when dormant magical abilities suddenly manifest, attracting the attention of a corrupt monarchy that views unsanctioned magic as a threat to their power. With only a loyal friend and a mysterious mentor, the farmer must navigate political intrigue, evade mage-hunters, and decide whether to hide, flee, or spark a revolution.

**Best For:** Players who enjoy underdog stories, political intrigue, and the classic hero's journey with magical awakening.

## Using Scenarios

To use any scenario:

1. Copy the desired scenario file to the root `parameters.yml`:
   ```bash
   cp scenarios/[scenario-name].yml parameters.yml
   ```

2. Generate the adventure:
   ```
   Prompt: generate-adventure.md
   ```

3. The adventure will be created with all the pre-configured settings.

## Creating Custom Scenarios

Feel free to save your own interesting parameter combinations here. Use descriptive filenames that indicate the theme and core concept (e.g., `fantasy-dragon-prophecy.yml` or `horror-cosmic-lighthouse.yml`).

## Scenario Design Notes

Each scenario balances several factors:
- **Event count** affects pacing and story arc
- **Party size** influences group dynamics and complexity
- **Token distribution** shapes whether encounters are combat, social, or exploration focused
- **Evolution rates** determine how much characters change during the adventure

The scenarios use different complexity distributions to create varied gameplay rhythms - some build slowly to climactic finales, while others maintain consistent tension throughout.