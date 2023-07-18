# Per Conversation
## Start
A new `GameController` is initialised using the `EventData` for the selected conversation. This involves:
1) Setting sound and player sprites based on `flowState`.
2) Sets up the `IGamePlayer`s for the player and NPC. This holds the AI for the NPC, and the UI interaction for the player.
3) Create a new `GameRunner` for the conversation, during which the only important step is setting up the new `Game`:
    1) Sets up the anchor card
    2) Makes a new `Player` for the player, then for the NPC, which involves shuffling the deck using `ShuffleInPlace` unless the event is the very first conversation with Elias before Mom shows up.
        - **Note:** this means the player's deck is shuffled before the NPC's deck.

Next, the initial hand is drawn by dequeuing cards from the end of the deck and appending them to the hand.

## Conversation Section
After the initial setup of a conversation, the decks are never shuffled again. Instead, the deck acts as a queue, and the following basic cycle is followed:
1) Player places a card. A card is dequeued from the player's deck to refill their hand.
2) NPC [[#AI Card Choices|chooses]] and places a card. A card is dequeued from the NPC's deck to refill their hand.
3) Repeat 1 and 2 until concordance or discordance occurs.
4) Display the correct text and increment the relevant counter (concordance or discordance).
5) Enqueue cards to both player's decks in order of the displayed sequence (left to right), except for the most recently played card, which becomes the anchor.

In the event of a *Reconsider* card being played, the player's current hand is enqueued to the deck from left to right, and then a new hand is drawn from the top of the deck.

In the event of a *Prepare* card being played:
- the player is simply presented with the entire contents of the `deck` at the time of playing the card, which means the entire deck except for the player's hand and any cards that are currently visible as played.
- the NPC takes a copy of this same `deck` list for their deck, shuffles it **(using important random)** then chooses the first card that has an `Input` or `Output` set that is not completely contained by the inputs or outputs (respectively) of cards currently in their hand. If no such card exists, they just take the first card in the shuffled list.

In the event of a *Backtrack* card being played, or a mismatch occurring that hits an *Accord* (as opposed to just causing a strike), the cards that are removed during the collapse are enqueued back to the deck in left to right order of the display.


### AI Card Choices
The NPC AI is not particularly complicated, though the various effects cards can have means there's a significant sequence of conditions.

The NPC first looks at each card in their hand and determines what it will become if they play that card. This allows the AI to account for *Accommodate* and *Elaborate* effects on cards in their hand.

They then sort this "preview" hand by two criteria:
1) If this NPC has the `prefersDoubles` flag, a card that would match when played after itself will be preferred over one that wouldn't.
    - In particular, this flag is set for:
        - Aurora
        - Diva
        - Elias (both normally and in Epilogue)
        - Isabella
        - Matilde
        - Mimi
        - Rohit
        - Samuel
        - Thunder
        - XN-220
2) If the NPC can see any of the player's hand due to having played an *Observe* card, cards that can be successfully followed by a card the NPC knows the player has will be preferred over ones that can't.
They will plan to choose the first card in this sorted hand that won't cause a discordance, then continue through the later checks. If there is no card that won't cause a discordance when played normally, they don't plan any card yet.

If the planned card (if there is one) has the *Clarify* effect, the NPC will plan to choose the earliest valid location in the sequence to place it. Otherwise, they will plan to simply play it normally.

If there is no planned card, the NPC will then search through their entire sorted hand for the first card that has the *Clarify* effect and can be placed anywhere in the sequence. If such a card and position are found, they become the planned card and position.

If there is still no planned card, the NPC will search through the sorted hand for the first card that has the *Backtrack* effect and will match at some point in the sequence, and plan that card.

If there is still no planned card, they search for the first card that has the *Reconsider* effect and plan that one.

At this point, if there is still no planned card, they simply plan for the first card in the sorted hand.

Now, if the planned card **does not** have the *Chatter* effect, the NPC will play the planned card in the planned position (at the end for all cards except *Clarify*).

If the planned card **does** have the *Chatter* effect, the NPC will check whether they have a valid card already in their hand to follow it up. This check does not account for effects on the follow-up card, simply checking whether the symbols will match, presumably because when the follow-up card actually needs to be chosen this whole process runs again.

If they do have a valid card to follow-up the planned *Chatter* card, they will play it as planned, otherwise they will choose a random card **(using important random)** from their hand to play.

# Between Conversations
==TODO==