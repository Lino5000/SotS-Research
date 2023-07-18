**First:** Can we get all items in one run (5 cycles)?

This is the list of all items, and how you can get them:
- **chocolate:** 
    - Concordance with Miriam
- **canal chilies:** 
    - Concordance with Oscar at the Canal, before landmines 'appear'
- **canned fish:** 
    - Concordance with Suzanne pre-cataclysm
    - Concordance with Tariq during first introduction, during the protest post-cataclysm, and after the protest if there isn't a riot.
- **dried fruit:** 
    - Concordance with Theo, except the time he gives you the letter to Mimi instead.
- **fish pie:** 
    - Concordance with Talia
- **licorice:** 
    - Concordance with Isabella
- **pickles:** 
    - Concordance with Tosuto, except pre-competition (cycle 2) where he just takes the Vinegar. If during competition, need to give him Vinegar on a Concordance to get Pickles.
- **roasted nuts:** 
    - Concordance with Alexis pre-calamity, except for if they are robbed that cycle.
    - Discordance with Alexis when they start selling crickets. 
    - Concordance with Alexis once they've moved to Bukam Boro.
    - Concordance with Klaus in Clifton if she's the initial character there.
    - Concordance with Klaus in the Oasis, if she robbed Alexis.
- **spice sampler:** 
    - Concordance with Maya at introduction. 
    - Concordance with Maya after meeting Lars (snitching on Lars in the process)
    - Important: not available post-cataclysm
- **vinegar:** 
    - Concordance with Haruto pre-cataclysm
    - Concordance with Haruto post-cataclysm if XN-220 has regained their memories.
- **matcha:** 
    - Concordance with Matilde in intro, unless it's the first cycle and you aren't with the caravan.
    - Concordance with Matilde, except when distracting her for Klaus, and when she is mourning Miriam.
- **bartow keyring:** 
    - Always received from Elias at the end of the first loop.
    - Depending on many factors, Elias may give you a keyring in the Epilogue.
- **succulents:** 
    - Concordance with Mimi when not bringing news from Big Basilio
- **synthesizer:** 
    - Concordance with Big Basilio during cycle 2
- **mobile phone:** 
    - Concordance with Big Basilio in cycle 1
    - Concordance after freeing Ramir
- **roasted crickets:** 
    - Concordance with Alexis in 3rd or 4th cycle.
    - Discordance with Alexis once they move to Bukam Boro.
- **painting:** 
    - Concordance with Tomas, except after he decides to stay in Pachenco (moving to Clifton means he can give painting again).
- **nibbled chocolate:** 
    - Concordance with Lil' Basilio
- **lamprey:** 
    - Concordance with Deion pre-cataclysm, except during the Cast-off.
    - Concordance with Thunder in Old Marae.
- **red wine:** 
    - Concordance with Marques
- **marigolds:** 
    - Concordance with Lars pre-cataclysm
- **kimchi:** 
    - Concordance with Salem
- **viola:** 
    - Concordance with Aurora on cycle 2.
- **ukulele:** 
    - Concordance with Aurora on cycle 1.
- **drum:** 
    - Concordance with Aurora on cycle 3 or 5, except during the performance.
- **scrap:** 
    - Concordance with Big Basilio after cycle 2.
    - Concordance with Mimi after moving to Anka.
    - Concordance with Thunder in Anka.
    - Concordance with Lil' Basilio while looting, if you don't already have scrap.
    - Any outcome when Oscar breaks.
    - Concordance with Tariq while preparing for the Cast-off.
    - Discordance with Tariq when asking to repair Oscar.
- **bar soap:** 
    - Concordance with Ophelia in intro, during railroad opening celebration, and during her story resolution.
- **caladiums:** 
    - Concordance with Masha in cycle 5, if you brought back materials for her and the store is successful.

Note that I didn't include all the items that you can get back from Klaus after she steals them from you, as that isn't really a source of new items anyway.


From these, we can determine the story checks, locations, or other tricky situations that are absolutely required for certain items:
- Tosende Canals - need to get here before the cataclysm to get chillies from Oscar, the spice sampler from Maya, and the marigolds from Lars.
- Old Marae - need to talk to Tariq, Talia, and Deion.
    - May be preferable to wait for the cataclysm, if possible, so nothing gets stolen by Gull.
    - Never mind, Deion won't give the Lamprey post-cataclysm.
- Desert Oasis - need dried fruit from Theo.
    - 
- Long Gate - need Succulents from Mimi.
    - Can get both location and road from `bigbasilio_railroad` if already have Desert Oasis.
    - Can get both location and road from `theo_cataclysm` or `theo_update`
    - Can get just one from `theo_resolution`
- Big Basilio - Must talk to on cycle 2 for the Synthesizer.
    - Also need to talk to on cycle 1 for Mobile Phone, otherwise we have to free Ramir. Unfortunately seems to be impossible, so freeing Ramir it is.
- Ramir - Need to get the Mobile Phone he gives after saving him.
    - Need concord in `gull_caravan` {5, 5, 5} (enter Old Marae with the caravan in Cycle 3), then concord in `ramir_free` {4, 4, 4} (talk to Ramir immediately after).
- Alexis - Talk to in both first (or second) and third (or fourth) cycles for both Nuts and Crickets.
- Aurora - Talk to in cycles 1, 2 and 3 or 5 for the Ukulele, Viola, and Drum respectively.
    - Can always unlock Aurora cycle 1 by talking to whichever of Salem or Tosuto shows up in Aldhurst. Nevermind, not true; misinterpreted the Ink code.
- Store Success - needed for Masha to give you the Caladiums.
    - This is difficult to avoid since we get so many items.
- Ophelia - Only ways to get Ophelia are `bigbasilio_second`, `lilbasilio_second`, and `bigbasilio_celebration`. The first two are inaccessible without being in Anka in Cycle 1. The third one only gives Ophelia if you already have Lil' Basilio.
- Miriam - Seems to be *very* difficult to have appear; only things I can find are 1) She's the initial NPC in Anka, 2) Discordance with Lil' Basilio in Cycle 2 before generating Big Basilio, or 3) concordance in `ophelia_second` while Big Basilio hasn't generated, or you haven't spoken to Elias about the roadshow.

## Character Considerations
- In Pachenco, one of Isabella, Tomas, or Marques will appear first. 
    - If Marques is first a Concordance in her second conversation will unlock both Isabella and Tomas at the same time (Start of last sequence). Make sure you get Concordance on the first conversation, since Discordance will make her mad and stop you from talking to her again. This takes 44 cards over 2 cycles.
        - Cycle 1: `marques_intro`: {5, 5, 5} concord, get Wine
        - Cycle 2: `marques_second`: {5, 5, 5} concord, get Tomas and Isabella (and Wine again)
        - Cycle 2: `tomas_intro`: {4, 4} concord, get Painting
        - Cycle 2: `isabella_rival`: {3, 3} concord, get Licorice
    - If Tomas is first, both others will be unlocked by Concordances with him eventually, but they unlock one at a time (Marques first) so it takes 48 cards over 3 cycles. Concordances are faster in all of his conversations.
        - Cycle 1: `tomas_intro`: {4, 4} concord, get Painting, activate Art show.
        - Cycle 2: `tomas_second`: {4, 4} concord, get Marques (and Painting again)
        - Cycle 2: `marques_intro`: {5, 5, 5} concord, get Wine
        - Cycle 3: `tomas_festival`: {4, 4} concord, get Isabella (and Painting again)
        - Cycle 3: `isabella_festival`: {3, 3, 3} concord, get Licorice
    - If Isabella is first, a concordance on the second conversation will unlock Marques, and then a Discordance with Isabella on the third conversation will unlock Tomas. This takes 44 cards over 3 cycles.
        - Cycle 1: `isabella_licorice`: {3, 3} concord, get Licorice
        - Cycle 2: `isabella_rival`: {3, 3} concord, get Marques (and Licorice again)
        - Cycle 2: `marques_intro`: {5, 5, 5} concord, get Wine
        - Cycle 3: `isabella_festival`: {3, 3, 3} discord, get Tomas
        - Cycle 3: `tomas_festival`: {4, 4} concord, get Painting
- We need to get to Aldhurst in all of the first 3 cycles to talk to Aurora, so we need to refuse to take Ramir to Anka in Clifton first cycle. It shouldn't be necessary to get the location of Anka from him; it seems like there are a number of people in Old Marae and Tosende Canals that will give routes to Anka in Cycle 2.
- In Aldhurst, there are three options for the initial NPC: Aurora, Tosuto, and Salem. We need to get Aurora to get the Ukulele. We then get Tosuto in cycle 2, and he gives us Salem after one success. Note that we need the cycle 2 conversations with Aurora and Tosuto to happen *before* the competition for this to work. The sequence of events is:
    - Cycle 1: `aurora_intro`: {4, 4} concord, Get Ukulele
    - Cycle 2: `aurora_mom`: {4, 4} concord, Get Viola and Tosuto
    - Cycle 2: `tosuto_precomp`: {4, 4} concord, Get Salem (and Haruto if he wasn't initial in Rimina)
    - Cycle 2: `salem_competition`: {4, 4} concord, Get Kimchi
    - Cycle 3: `tosuto_mystery`: {4, 4, 4} concord, Get Pickles
- We need to get to Anka in cycle 2 to get all the characters we need. Because we can't get to Anka in the first cycle, we need Miriam to be the initial character; there's not enough time to unlock her otherwise. The sequence of events to unlock everyone else is:
    - Cycle 2: `miriam_travel`: {4, 4} concord, get Chocolate and Lil' Basilio
    - Cycle 2: `lilbasilio_intro`: {5, 5} concord, get Big Basilio and Nibbled Chocolate
    - Cycle 2: `bigbasilio_intro`: {4, 4} concord, get Synthesizer
    - Cycle 3: `bigbasilio_celebration`: {4, 4, 4} concord, get Ophelia and Scrap
    - Cycle 3: `ophelia_celebration`: {5, 5, 5} concord, get Soap
- We have to get into Old Marae pre-cataclysm, otherwise Deion won't give us Lamprey. Besides Gull, there are three possible initial characters; Deion, Talia, and Tariq.
    - Deion
        - Cycle 2: `deion_intro`: {3, 3} concord, get Lamprey, Talia, and Tosende Canals.
        - Cycle 2: `talia_fish`: {4, 4} concord, get Fish Pie.
        - Cycle 3: `deion_compete` or `deion_during`: {3, 3, 3} concord, get Tariq (and maybe Lamprey Again)
        - Cycle 4: `tariq_protest`: {4, 4, 4} concord, get Canned Fish
    - Talia
        - Cycle 2: `talia_fish`: {4, 4} concord, get Fish Pie, Deion, and Tosende Canals
        - Cycle 2: `deion_intro`: {3, 3} concord, get Lamprey
        - Cycle 3: `deion_compete` or `deion_during`: {3, 3, 3} concord, get Tariq (and maybe Lamprey Again)
        - Cycle 4: `tariq_protest`: {4, 4, 4} concord, get Canned Fish
    - Tariq
        - Cycle 2: `tariq_trash`: {4, 4} concord, get Canned Fish, Talia, and Tosende Canals
        - Cycle 2: `talia_fish`: {4, 4} concord, get Fish Pie, Deion
        - Cycle 2: `deion_intro`: {3, 3} concord, get Lamprey
- The other consideration with Old Marae is that we must enter it with the caravan in Cycle 3 to prevent Ramir's arrest, so we can get the Mobile Phone.
    - Cycle 3: `gull_caravan`: {5, 5, 5} concord, save Ramir
    - Cycle 3: `ramir_free`: {4, 4, 4} concord, get Mobile Phone
- We need to get to Tosende Canals in cycle 2 to talk to all the people there. Note that we can't get to Tosende Canals before Cycle 2 because we can't get through Old Marae. There are three possible initial characters; Lars, Maya and Oscar. We need to get Maya or we won't be able to get the others' items before the Cataclysm.
    - Cycle 2: `maya_welcome`: {4, 4, 4} concord, get Spice Sampler, Oscar and Road to Anka
    - Cycle 2: `oscar_welcome`: {3, 4} concord, get Chillies
    - Cycle 3: `maya_inspect`: {4, 4, 4} either (pass first sequence), get Lars
    - Cycle 3: `lars_intro`: {4, 4} concord, get Marigolds

# The Route

Taking into account the story requirements for obtaining each item, this is an efficient option for collecting all of them in a single game:

## First trip
Follow the caravan to start with. Make sure you talk to as many people who can give items as possible. This means:
- In Pachenco, talk to whichever of Isabella, Marques, or Tomas shows up to get Licorice, Wine, or Painting respectively, then talk to Nadine for the next road.
- In Clifton, talk to Alexis (or Klaus if she's there instead) to get the Nuts, and to Ramir to get the next part of the Route.
- In Bukam Boro, grab the Matcha from Matilde, then talk to Nadine to get the route to Aldhurst.
- In Aldhurst, there are three characters that can show up; Tosuto, Salem, and Aurora. If you don't get Aurora, **your run is dead**. So yay, 1/3 RNG check that just immediately kills the run if you don't get it. Talk to Aurora and get the Ukulele and a right-side diamond card, then talk to Nadine to finish the caravan loop.
- Back in Bartow, talk to the Stranger to get a card ready for manipulating Nadine, then talk to Elias to get the Keyring before unpacking to avoid the "Hey" animation.

## Second trip
We follow the caravan again to get the full route.