Stateful firewalls keep track of some form of state in between packets

Stateless Firewalls in [[TCP]] 
	Every connection has both a request and response portion (2 rules needed)
	You need a rule that covers the response ephemeral ports (need to cover port range)
Stateful
	You only need one rule for TCP because you only have to allow or deny the request.
