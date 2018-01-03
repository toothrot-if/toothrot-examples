# Cloak of Darkness

## default

(#) background: "linear-gradient(to bottom, rgba(230, 230, 230, 1) 0, rgba(140, 140, 140, 1) 30%, rgba(0, 0, 0, 1) 95%)"

### start

(#) reveal: false

The Cloak of Darkness
=====================

*Based on Roger Firth's original. Ported to Toothrot and extended by Jonathan Steinbeck.*

Click to start the game.

***

(#) autonext: 7000

Your sightseeing tour of the city takes a sudden turn for the worse when it starts to rain
heavily.

***

(#) autonext: 8000

As you look for shelter, you silently scold yourself for not bringing along an umbrella tonight.

***

(#) autonext: 6000

When your sight falls on the entrance of an old opera house, you don't hesitate to enter.

(>) foyer


### foyer

```js @entry
_.event(_.oneOf(
    "",
    "The sound of rain pattering against the windows.",
    "Through the windows you see a car driving past the opera house.",
    "Clouds of dust dance in the majestic chandeliers light above.",
    '"Why is no one here?" you think.',
    '"Hellooo? Is someone here?"',
    "Outside, the sign on the facade flickers back to life for just a second, " +
        "engulfing the entrance in neon blue light."
));
```

(#) tags: ["room"]

Foyer
-------------

The dimly lit foyer of the opera house. It is devoid of people and furniture. An entrance
leads to the [street](#exit_opera_house) outside.

There are doorways [west](#cloakroom) and [south](#bar).


### exit_opera_house

You only just arrived. And besides, it's still raining outside.

(<)


### cloakroom

```js @entry
_.event(_.oneOf(
    "",
    "",
    "",
    "The floor boards creak as you shift your weight from one foot to the other.",
    "The light on the ceiling flickers, then resumes its normal function."
));
```

(#) tags: ["room"]

Cloakroom
----------------

A small room with walls that were clearly lined with hooks in a distant past, of which
now only one [hook](#hook) remains.

The [foyer](#foyer) is to the east.


### hook

A small brass hook.

(@) !used ??? Hang your cloak here => hang_cloak_on_hook
(@) used ??? Take the cloak and wear it => take_and_wear_cloak

(<)


### hang_cloak_on_hook

```js @entry
_.node("hook").be("used");
_.node("cloak").moveTo("hook");
```

You take off your cloak and hang it on the hook.

(<)


### take_and_wear_cloak

```js @entry
_.node("hook").dontBe("used");
_.node("cloak").moveTo("you");
```

You take the cloak from the hook and put it on.

(<)



### cloak

```js @brief
_.self().isIn("hook") ? "Your {cloak} hangs here." : "You're wearing a handsome {cloak}."
```

A fashionable cloak, made of velvet and satin. Its blackness is so deep
that it almost seems as though it absorbs the light around it.

(<)


### bar

(#) tags: ["room"]

```js @entry
if (_.node("you").contains("cloak")) {
    _.skipTo("unlit_bar");
}
```

The Bar
-------------

Now that you got rid of your light-absorbing cloak, you can see that this room once
served as a bar.

Someone has scribbled a [message](#message) in the dust on the floor.


### message

```js @message
$.stumbles >= 3 ? "You lose." : "You win."
```

The message reads:

**`@message`**


### unlit_bar

(#) tags: ["room"]

Dark Room
--------------

This room is pitch black and [you](#you) can't even see your own hands. The only
light here is coming from the [foyer](#foyer) doorway, but it's not enough
to see what kind of room this is.

Maybe there's a light switch somewhere? [You](#you) could try going
[west](#stumble_in_darkness), [east](#stumble_in_darkness) or [south](#stumble_in_darkness)
anyway and hope not to trip over something.


### stumble_in_darkness

```js @entry
$.stumbles = ($.stumbles || 0) + 1;
```

You stumble around in the darkness until your foot hits a wall. Unfortunately,
you don't find a ligh switch anywhere.

(<)


### you

(#) contains: ["cloak"]

You're quite drenched from the rain and hope it will stop soon. You're also a little confused
about the fact that you're the only person in this big opera house.

(<) room
