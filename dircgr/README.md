# hpDIRC geometric reconstruction (DircGR) calibration files

Used by the EICrecon `DircGR` factory (`DIRC:DircGR`), fetched with the
geometry via epic `compact/calibrations.xml` into `calibrations/dircgr/`.

- `lut_bar{0..9}.root`: look-up tables, tree `dircLUT` (`ipixx`, `ipixy`,
  `npath`, `ipath`, `nOP`, `OPprob`, `OPdirx/y/z`, `OPtime`, `OPdirRMS`,
  `OPtimeRMS`). File `lut_bar{i}` holds DIRCHits cellID bar `i`. Pixels are
  the DIRCHits MCP readout cells (3.3 mm, 107 x 73 over the prism back face,
  cell (0,0) centred on the MCP plane): `ipixx = 53 - cellY`,
  `ipixy = cellX + 36`. For each pixel, the optical-photon paths from a
  point source 2 mm inside the prism-side end of the bar: unit direction at
  creation (in the bar), mean time to the MCP [ns], fraction of the pixel's
  photons (`OPprob`), and the spreads of the path. Paths are found by
  friends-of-friends grouping of 20M simulated photons per bar (3.18 eV,
  isotropic into the prism hemisphere).
- `chrcorr.root`: chromatic correction for the per-photon Cherenkov angle,
  TGraphs vs track polar angle [deg]:
  `gChrom{1,2}par{0,1}_Theta_0_0` (pol1 in dt/L used by DircGR; 1 = photons
  going directly to the prism, 2 = via the mirror) and
  `gchr{1,2}par{0,1}_Theta_0_0` (vs wavelength, truth diagnostics).
  Set `0_0` (pi+, 3 GeV) only, the DircGR default.

Geometry: epic with the DIRC changes of eic/epic#1226 (3.3 mm MCP pixels,
lenses centred on the bars and touching). The LUTs and the chromatic
correction must be regenerated when the bar/lens/prism/MCP geometry changes.

Generated with npsim (LUT: optical-photon gun per bar; chrcorr: pi+ 3 GeV
at 15 polar angles, 25-160 deg) and the DircGR calibration tools (LUT
builder; EICrecon `-PDIRC:DircGR:calibFile=...` dump + `chrcorrfit.C`), to
be published in the DircGR_Calibration repository. W.J. Llope.
