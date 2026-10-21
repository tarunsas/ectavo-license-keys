Ectavo license signing key
==========================

private.key  - signs every license. Keep it secret and back it up (password manager
               or encrypted USB). Lost: you cannot issue licenses that existing
               installs accept. Leaked: anyone can; you must ship a new public key.
public.key   - built into the app (LicenseKeys.PUBLIC_KEY in ectd-swing).
issued/      - licenses issued so far. Keep a record of each: licenseId, customer,
               installation ID, regions, users, expiry.

Running the tool: ectavo-license-gen.jar in this folder (rebuild it with
"mvn package" in ectd-swing; it lands in target/ectavo-license-gen.jar).

  G="java -jar ~/ectavo-license-keys/ectavo-license-gen.jar"

Issue a one-year license bound to a customer's installation (they find the
Installation ID under Help > License, or in the dialog shown at login):

  $G issue --key ~/ectavo-license-keys/private.key \
      --customer "Acme Pharma Ltd" --installation 7F3A-91C2-44DE-B805 \
      --regions US,EU,CA --users 5 --expires 2027-10-31 \
      --out ~/ectavo-license-keys/issued/acme-2026.lic

  Trial:      --regions ALL --days 30 --edition Trial
  Perpetual:  --perpetual instead of --days/--expires
  Any install: leave out --installation (use for your own testing only)
  Regions:    US, EU, JP, CA, AU, GCC, ZA, WA or ALL; --users 0 or omitted = no limit
              (GCC = Gulf Cooperation Council, ZA = South Africa/SAHPRA, WA = ECOWAS/WAHO)

Check a file:  $G show some.lic

The customer installs it with Help > License > Load license file...; it is copied
to ~/.ectavo/license.lic on their machine. Renewing = issue a new file with a
later expiry; they load it the same way.

issued/dev-unbound.lic is an all-regions 30-day license for any installation,
for testing the app yourself (expires 12 Nov 2026).
