# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.4.3] - 2021-12-27

### Deps

- Update the acceptable range for tracing-distributed to include 0.4

### Additions

- Implemented Error for `ParseSpanIdError`

## [0.4.2] - 2021-06-28

### Fixes

Previously `parent_id` and `span_id` spans were incorrectly prefixed with `span-`.
Honeycomb interprets this fine for `span_id` but gets confused by it in `parent_id`.

This release removes the `span-` prefix in these as it causes issues.

## [0.4.1] - 2021-05-25

(0.4.0 was yanked as it was done from the wrong git commit.)

### Additions
- New `Builder` struct for constructing the `hOneycombTelemetry` instance, which now supports multiple reporting backends.
- New `StdoutReporter` backed for use in AWS Lambda and similar environments.
    - See https://docs.honeycomb.io/getting-data-in/integrations/aws/aws-lambda/

## [0.4.0] - 2021-05-25

_(Yanked, wrong git commit)_

## [0.3.0] - 2021-04-15

### Changes
- Full rework of `TraceId`.
  - Allows `TraceId`s to be any arbitrary string, as the honeycomb ecosystem expects.
  - Adds many ways of converting to and from `TraceId`s.
- Rework of `SpanId`.
  - Instance Ids have been removed, as they are unnecessary.
  - `SpanId` serialization formatting is now in hexadecimal.
- Changed to send `duration_ms` as an `f64`, as honeycomb expects.
    - This allows for sub-millisecond span timing.

### Additions
- Trace-level sampling.
- `parking_lot` feature.

### Fixes
- Fixes a deadlock where libhoney's reponses channel was not being consumed.
    - See [`9dd18b55ea`](https://github.com/eaze/tracing-honeycomb/commit/9dd18b55ea96b95ce76d0051dbcbd085b7e7f2f1) for much more information.
- Always sends traces if no sampling is set.
- Sampling is now deterministic for a given `TraceId`.
- Properly set the `timestamp` field in libhoney.
- Relaxed dependency constraints.

(These were also included in the 0.2.1-eaze.X versions.)

## Pre-0.3.0

Changelogs not kept, please see git history.
