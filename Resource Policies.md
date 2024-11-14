A type of security Policy

Applied to a resource instead of a user
Has an additional field `Principal` that tells us which identities this resource policy will allow/deny. We do not need this in non resource policies because it is implicit.

If we use the wildcard `"Principal": *` it will cover all users, even anonymous ones