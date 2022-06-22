# What is the Forwarding Argument?

### Reference: 7.4.2 Forwarding Argument

## Summary
1. Motivation:
    - Passing arguments unchanged through an interface is an important use of variadic templates.
    - Consider a notion of a network input channel for which the actual method of moving values is a parameter. Different transport mechanisms have different sets of constructor parameters [1].
    - Move arguments unchanged from the **InputChannel** constructor to **Transport** constructor.

~~~c++
template<typename Transport>
    requires concepts::InputTransport<Transport>
class InputChannel{
public:
    //...
    InputChannel(TransportArgs &&... transportArgs)
    :_transport(std::forward<TransportArgs>(transportArgs)...)
    {}
    // ...
    Transport _transport;
}
~~~

### Date
2022/06/22