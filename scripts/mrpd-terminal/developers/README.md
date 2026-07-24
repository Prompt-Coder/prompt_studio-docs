---
description: Extend the terminal — write adapters for any backend, understand the design
icon: code
---

# For Developers

The terminal is built to be extended. Our position: **be transparent about our layer, protect other people's layers.**

* The **adapter contract** (`shared/adapter_interface.lua`) and the **framework contract** (`framework/_registry.lua`) ship **open** — you can't target an API you can't read.
* `adapters/qb_policejob.lua` ships **open** as the complete reference implementation; `adapters/showcase.lua` and `adapters/null.lua` are open teaching examples.
* `config.lua`, `fxmanifest.lua`, and your own adapter files stay plaintext in the escrowed build — custom adapters work against the shipped product.
* The wasabi / LB / p\_mdt adapters are escrowed because they embed export surfaces of *other developers'* paid scripts, shared with us for these integrations.

<table data-view="cards">
    <thead>
        <tr>
            <th>Title</th>
            <th>Description</th>
            <th data-card-target data-type="content-ref">Target</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><strong>Writing Adapters</strong></td>
            <td>The full guide — contract, capabilities, skeleton, golden rules, testing</td>
            <td><a href="writing-adapters.md">writing-adapters.md</a></td>
        </tr>
        <tr>
            <td><strong>Integrating Your MDT</strong></td>
            <td>MDT developer? What to provide for an official shipped adapter</td>
            <td><a href="mdt-integration.md">mdt-integration.md</a></td>
        </tr>
        <tr>
            <td><strong>Architecture</strong></td>
            <td>The three axes, request flow, and where the project is going</td>
            <td><a href="architecture.md">architecture.md</a></td>
        </tr>
    </tbody>
</table>

{% hint style="success" %}
**API stability promise:** the adapter contract only changes additively — new optional methods and capability keys may appear; existing names and shapes don't break. An adapter you write today is meant to keep working.
{% endhint %}
