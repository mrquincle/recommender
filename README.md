# Recommender engine

Expected input:

    [time (T), activity type (A), weather (W), temperature (M), gps location (X)]

What we want:

    P(A|T,W,M,L)

We assume that people can be clustered into groups of similar people. This similarity is with respect to their behavior
in the context of exercise. The number of possible groups can be obtained through a random process. There are different facets that can dictate which people belong to the same group. We can incorporate all different types - time, weather,
temperature, location - but this would rarely lead to useful clusters. A person always running at night will do this at
a totally different location as another person always running at night.

We use a Hierarchical Dirichlet Process to generate a set of group indicators `z_ik`, with `i` indicating the individual, and `k` the group. Due to the fact that this is a Dirichlet Process there is a not neglectable chance that the same group is selected for another person. For each group we have another Dirichlet Process which generates parameters, `theta`. This corresponds for example with time `T` in the dataset. It is also possible to generate parameters per individual where we disregard groups. In this case we generate from a Dirichlet Process without regard for in which group the individual might fall. Note, that in this case it is still possible that individuals get assigned the same parameter (again, there is a chance bigger than zero to select the same parameter value). The local parameters might be weather `W`, temperature `M`, and location `X`.

[1] Effective Mobile Context Pattern Discovery via Adapted Hierarchical Dirichlet Processes (2014) Zheng et al.




