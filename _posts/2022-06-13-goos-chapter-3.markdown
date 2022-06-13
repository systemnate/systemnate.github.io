---
layout: post
title:  "GOOS - Chapter 3"
date:   2022-06-13 12:35:00 -0500
categories: development testing goos
---

# Chapter 3

This post continues my reading and understanding of "Growing Object-Oriented
Software, Guided by Tests" by Steve Freeman and Nat Pryce.

Chapter 3 is really just a brief intro to the tools used in the book.  It ends
up with a Java example using JUnit, jMock, Hamcrest, etc.  Here is the test:

{% raw %}
```Java
@RunWith(JMock.class)
public class AuctionMessageTranslatorTest {
  private final Mockery context = new JUnit4Mockery();
  private final AuctionEventListener listener =
context.mock(AuctionEventListener.class);
  private final AuctionMessageTranslator translator = new
AuctionMessageTranslator(listener);

  @Test public void
  notifiesAuctionClosedWhenCloseMessageReceived() {
    Message message = new Message();
    message.setBody("SOLVersion: 1.1; Event: CLOSE;");

    context.checking(new Expectations() {{
      oneOf(listener).auctionClosed();
    }});

    // Note: not sure what UNUSED_CHAT is
    translator.processMessage(UNUSED_CHAT, message);
  }
}
```
{% endraw %}

When I first tried this book years back, I lacked the experience to take the
ideas and make them work appropriately with Ruby on Rails. Now that I have a little
more experience, I can take the ideas, not get bogged down by the exact
syntax, and map that into whatever language I use.

I translated this into Ruby/RSpec, and here is the result.
I haven't run this code, but it would be something like:

```Ruby
RSpec.describe AuctionTranslator do
  it 'notifies AuctionEventListener when a close message is received' do
    listener = spy('AuctionEventListener')
    translator = AuctionTranslator.new(listener)
    message = "SOLVersion: 1.1; Event: CLOSE"

    translator.process_message(message)

    expect(listener).to have_received(:auction_closed)
  end
end
```

A lot more readable, for sure. The passing implementation wasn't in the chapter, but I imagine the
implementation to make this pass would look something like:

```Ruby
class AuctionTranslator
  def initialize(listener)
    @listener = listener
  end

  def process_message(message)
    if message =~ /Event: CLOSE/
      @listener.auction_closed
    end
  end
end
```

The idea with this code is that we are testing an `AuctionTranslator` class that
interacts with an `AuctionEventListener` class. When we call #process_message on
the `AuctionTranslator` class, we want to send an #auction_closed message to the
`AuctionTranslator` class (or whatever class plays that role). This method is a
command method, so there is nothing to assert with the return value, but we
want to assert that the translator called the collaborator appropriately.

This completes Part I of the book. Part II is "The Process of Test-Driven
Development", which is divided into the following chapters:
- Kick-Starting the Test-Driven Cycle
- Maintaining the Test-Driven Cycle
- Object-Oriented Style
- Achieving Object-Oriented Design
- Building on Third-Party Code
