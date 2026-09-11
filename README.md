# Design for Equity Specs

Project-ready specifications for building products that don't quietly exclude the people they serve. Each spec turns a body of research into rules a team can design, build, and test against. The key words **MUST**, **SHOULD**, and **MAY** follow [RFC 2119](https://www.rfc-editor.org/rfc/rfc2119).

The specs are plain Markdown and framework-agnostic. They work as a design review checklist, a release gate, or context for a coding agent. Link one from your `README.md`, `CONTRIBUTING.md`, or `AGENTS.md` and hold the product to it.

## Equity

| Spec | Conformance target |
|---|---|
| [Bias audit](bias-audit-spec.md) | No shipped surface encodes a representational, linguistic, or structural bias against the population it serves. |
| [Gender bias](gender-bias-spec.md) | No decision, string, default, or rule disadvantages women, and no design assumes a male user, device owner, or staff member. |
| [Disability and ableism](disability-and-ableism-spec.md) | No decision, string, image, moderation rule, or model output treats disabled people as lesser, as inspirational, or as absent. |
| [Constrained path](constrained-path-spec.md) | The most constrained user in the audience completes every core task on the default path, with no separate lite edition. |
| [AI in design and product](ai-in-design-and-product-spec.md) | AI used in the product, and in building it, doesn't flatten the product toward its training-data defaults or become unaccountable to the person its output acts on. |

## Accessibility

| Spec | Conformance target |
|---|---|
| [WCAG 2.2 AA](WCAG-AA-spec.md) | WCAG 2.2 Level AA as project-ready rules. The baseline every web UI should meet. |
| [WCAG 2.2 AAA](WCAG-AAA-spec.md) | WCAG 2.2 Level AAA as project-ready rules, with a required format for documenting any criterion a view can't meet. |

The equity specs build on these. WCAG covers whether a screen is operable with assistive technology. The disability and ableism spec covers whether the product treats disabled people as equals, which a screen can fail while passing every WCAG criterion.
