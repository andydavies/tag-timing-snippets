# Timing Snippets for 3rd-Party Tags

Sometimes 3rd-Party tags provide content that's core to our visitors experience, other times they provide invisible features that allow us to get a better understanding of our visitors experience and how they behave.

Tags can have a crucial impact on visitor experience, yet that impact is difficult to measure as the tags themselves often provide no information on when their key milestones are reached.

We're often fallback to using the Resource Timing API to measure when components were fetched and how long they took to download but this tells us little about our visitors experience.

## Aims

This project aims to build a collection of snippets that can help measure tags more effectively and answer questions such as:

- When did our reviews service display the rating and reviews for a product?
- When did the anti-flicker snippet that our A/B testing tool recommends reveal the page?
- When did our IAB Consent Management Platform tell our advertising provider they could requests ads?
- When did adverts get displayed?

## Using

The examples so far all rely on `performance.mark` to record the point at which the event occured.  

This can be replaced with a call to an analytics or other product API as needed.  

## Contributing

If you've got ideas or examples on how to measure the impact of other 3rd-party tags I'm very open to contributions (there are so many tags out there)

Raise an issue if you've got a tag that you'd like to measure but don't know how.

## Supporting

If you find these snippets useful and want to say thanks or encourage me to add more, feel free to [Buy Me a Coffee](https://www.buymeacoffee.com/andydavies)

## License

All snippets are MIT Licensed.

