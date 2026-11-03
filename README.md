# Axe-Fx III LLM Controller Guide

A practical guide for building a safe Windows .NET LLM-to-MIDI control bridge for the Fractal Audio Axe-Fx III using OpenCode, USB MIDI, and GitHub Pages.

## Purpose

This project documents a controlled approach for using natural-language requests to operate approved Axe-Fx III functions.

The intended design is:


User request
    ↓
LLM interprets intent
    ↓
Approved command ID
    ↓
Local C#/.NET validation
    ↓
Known MIDI Program Change / Control Change sequence
    ↓
Fractal Audio Axe-Fx III


The LLM does not directly control hardware. A local C#/.NET application validates approved commands and sends only predetermined MIDI actions.

## Project Scope

This guide covers:

- Windows 10 or later setup
- Axe-Fx III USB MIDI configuration
- External Controller and modifier setup
- C#/.NET MIDI bridge development
- NAudio MIDI output
- OpenCode-assisted development workflow
- GitHub and GitHub Pages publication
- Optional LLM command interpretation using structured output
- Dry-run testing and safe live MIDI testing

## Safety Design Principles

This project uses an allowlisted-command model.

The controller should permit only known, tested actions such as:

- Program Change (`pc`)
- Control Change (`cc`)
- Wait/delay (`wait`)

The controller should reject:

- Unknown command IDs
- Arbitrary raw MIDI messages
- SysEx messages
- Preset writes or overwrites
- Factory resets
- Firmware actions
- Global I/O or routing changes
- Direct LLM access to MIDI output

## Recommended Architecture


Text or voice request
        ↓
LLM
        ↓
Structured command ID only
        ↓
C#/.NET validation layer
        ↓
Approved MIDI message sequence
        ↓
Axe-Fx III over USB MIDI


## Development Tools

- Windows 10 or later
- Fractal Audio Axe-Fx III
- Axe-Fx III USB driver
- Axe-Edit III
- Fractal-Bot
- .NET 10 SDK
- C#
- NAudio
- OpenCode
- GitHub Pages

## Suggested Initial Commands

Start with a small number of tested commands:


clean_rhythm
lead
ambient_lead
delay_low
delay_high


Do not add more advanced functions until direct MIDI control is reliable.

## Recommended Development Sequence

1. Back up Axe-Fx III system settings and relevant presets.
2. Configure USB MIDI and one External Controller.
3. Build a deterministic C#/.NET MIDI bridge.
4. Test MIDI port discovery.
5. Test commands in dry-run mode.
6. Test one Program Change and one Control Change live at low volume.
7. Commit the working direct-MIDI baseline.
8. Add optional LLM interpretation.
9. Test unclear and unsupported requests.
10. Add new commands one at a time.

## Important Notes

- Do not store API keys in source code, `config.json`, screenshots, or Git commits.
- Do not publish proprietary presets, backups, personal information, or sensitive configuration data.
- Keep a physical Axe-Fx III front-panel or foot-controller fallback available.
- Use this project as a guide; validate all MIDI assignments, preset numbers, and controller mappings on your own equipment.


## Disclaimer

This is an independent community project and is not affiliated with, endorsed by, or supported by Fractal Audio Systems or OpenAI.
