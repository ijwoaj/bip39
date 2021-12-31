<!DOCTYPE html>
<html>
    <head lang="en">
        <meta charset="utf-8" />
        <title>BIP39 - Mnemonic Code</title>
        <link rel="stylesheet" href="css/bootstrap.css">
        <link rel="stylesheet" href="css/app.css">
        <meta content="Mnemonic code for generating deterministic keys" name="description"/>
        <meta content="width=device-width, initial-scale=1.0" name="viewport" />
        <meta content="bitcoin mnemonic converter" name="description" />
        <meta content="Ian Coleman" name="author" />
        <link type="image/x-icon" rel="icon" href="data:image/x-icon;base64,iVBORw0KGgoAAAANSUhEUgAAABAAAAAQEAYAAABPYyMiAAAABmJLR0T///////8JWPfcAAAACXBIWXMAAABIAAAASABGyWs+AAAAF0lEQVRIx2NgGAWjYBSMglEwCkbBSAcACBAAAeaR9cIAAAAASUVORK5CYII=" />
    </head>
    <body>
        <div class="container">

            <h1 class="text-center">Mnemonic Code Converter</h1>
            <p class="version">v0.5.4</p>
            <hr>
            <div class="row">
                <div class="col-md-12">
                    <h2>Mnemonic</h2>
                    <form class="form-horizontal" role="form">
                        <div class="form-group">
                            <div class="col-sm-2"></div>
                            <div class="col-sm-10">
                                <p>You can enter an existing BIP39 mnemonic, or generate a new random one. Typing your own twelve words will probably not work how you expect, since the words require a particular structure (the last word contains a checksum).</p>
                                <p>
                                    For more info see the
                                    <a href="https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki" target="_blank">BIP39 spec</a>.
                                </p>
                            </div>
                        </div>
                        <div class="form-group generate-container">
                            <label class="col-sm-2 control-label"></label>
                            <div class="col-sm-10">
                                <div class="form-inline">
                                    <div class="input-group-inline">
                                         <span>Generate a random mnemonic</span>:
                                        <button class="btn generate" ><b>GENERATE</b></button>
                                        <select id="strength" class="strength form-control">
                                            <option value="3">3</option>
                                            <option value="6">6</option>
                                            <option value="9">9</option>
                                            <option value="12">12</option>
                                            <option value="15" selected>15</option>
                                            <option value="18">18</option>
                                            <option value="21">21</option>
                                            <option value="24">24</option>
                                        </select>
                                        <span>words, or enter your own below</span>.
                                        <p class="warning help-block hidden">
                                            <span class="text-danger">
                                                Mnemonics with less than 12 words have low entropy and may be guessed by an attacker.
                                            </span>
                                        </p>
                                    </div>
                                </div>
                            </div>
                        </div>
                        <div class="entropy-container hidden">
                            <div class="form-group text-danger">
                                <label class="col-sm-2 control-label">Warning</label>
                                <div class="col-sm-10 form-control-static">
                                    <span>Entropy is an advanced feature. Your mnemonic may be insecure if this feature is used incorrectly.</span>
                                    <a href="#entropy-notes">Read more</a>
                                </div>
                            </div>
                            <div class="form-group">
                                <label for="entropy" class="col-sm-2 control-label">Entropy</label>
                                <div class="col-sm-7">
                                    <textarea id="entropy" rows="2" class="entropy private-data form-control" placeholder="Accepts either binary, base 6, 6-sided dice, base 10, hexadecimal or cards" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                                    <div class="row filter-warning text-danger hidden">
                                        <p class="col-sm-12">
                                        <strong>
                                        Some characters have been discarded
                                        </strong>
                                        </p>
                                    </div>
                                    <div class="row">
                                        <label class="col-sm-3 control-label"><span class="more-info" title="Based on estimates from zxcvbn using Filtered Entropy">Time To Crack</span></label>
                                        <div class="crack-time col-sm-3 form-control-static"></div>
                                        <label class="col-sm-3 control-label">Event Count</label>
                                        <div class="event-count col-sm-3 form-control-static"></div>
                                    </div>
                                    <div class="row">
                                        <label class="col-sm-3 control-label">Entropy Type</label>
                                        <div class="type col-sm-3 form-control-static"></div>
                                        <label class="col-sm-3 control-label">Avg Bits Per Event</label>
                                        <div class="bits-per-event col-sm-3 form-control-static"></div>
                                    </div>
                                    <div class="row">
                                        <label class="col-sm-3 control-label">Raw Entropy Words</label>
                                        <div class="word-count col-sm-3 form-control-static"></div>
                                        <label class="col-sm-3 control-label"><span class="more-info" title="Total bits of entropy may be less than indicated if any entropy event uses a weak source.">Total Bits</span></label>
                                        <div class="bits col-sm-3 form-control-static"></div>
                                    </div>
                                    <label class="col-sm-3 control-label">Filtered Entropy</label>
                                    <div class="filtered private-data col-sm-9 form-control-static"></div>
                                    <label class="col-sm-3 control-label">Raw Binary</label>
                                    <div class="binary private-data col-sm-9 form-control-static"></div>
                                    <label class="col-sm-3 control-label">Binary Checksum</label>
                                    <div class="checksum private-data col-sm-9 form-control-static">&nbsp;</div>
                                    <label class="col-sm-3 control-label">Word Indexes</label>
                                    <div class="word-indexes private-data col-sm-9 form-control-static">&nbsp;</div>
                                    <label class="col-sm-3 control-label">Mnemonic Length</label>
                                    <div class="col-sm-9">
                                        <select class="mnemonic-length form-control">
                                            <option value="raw" selected>Use Raw Entropy (3 words per 32 bits)</option>
                                            <option value="12">12 <span>Words</span></option>
                                            <option value="15">15 <span>Words</span></option>
                                            <option value="18">18 <span>Words</span></option>
                                            <option value="21">21 <span>Words</span></option>
                                            <option value="24">24 <span>Words</span></option>
                                        </select>
                                        <p class="weak-entropy-override-warning hidden">
                                            <span class="text-danger">
                                                The mnemonic will appear more secure than it really is.
                                            </span>
                                        </p>
                                    </div>
                                    <label class="col-sm-3 control-label">PBKDF2 rounds</label>
                                    <div class="col-sm-9">
                                        <select class="pbkdf2-rounds form-control" style="width: 60%;float: left;">
                                            <option value="2048" selected>2048 <span>(compatibility)</span></option>
                                            <option value="4096">4096 <span>iterations</span></option>
                                            <option value="8192">8192 <span>iterations</span></option>
                                            <option value="16384">16384 <span>iterations</span></option>
                                            <option value="32768">32768 <span>iterations</span></option>
                                            <option value="custom">Custom <span>iterations</span></option>
                                        </select>
                                        <input type="number" class="form-control hidden" id="pbkdf2-custom-input" value="1" min="1" pattern="[0-9]" style="float: right;width: 40%;">
                                    </div>
                                </div>
                                <div class="col-sm-3">
                                    <p>Valid entropy values include:</p>
                                    <ul>
                                        <li>
                                            <label>
                                                <input type="radio" name="entropy-type" value="binary">
                                                <strong>Binary</strong> [0-1]<br>101010011
                                            </label>
                                        </li>
                                        <li>
                                            <label>
                                                <input type="radio" name="entropy-type" value="base 6">
                                                <strong>Base 6</strong> [0-5]<br>123434014
                                            </label>
                                        </li>
                                        <li>
                                            <label>
                                                <input type="radio" name="entropy-type" value="dice">
                                                <strong>Dice</strong> [1-6]<br>62535634
                                            </label>
                                        </li>
                                        <li>
                                            <label>
                                                <input type="radio" name="entropy-type" value="base 10">
                                                <strong>Base 10</strong> [0-9]<br>90834528
                                            </label>
                                        </li>
                                        <li>
                                            <label>
                                                <input type="radio" name="entropy-type" value="hexadecimal" checked>
                                                <strong>Hex</strong> [0-9A-F]<br>4187a8bfd9
                                            </label>
                                        </li>
                                        <li>
                                            <label>
                                                <input type="radio" name="entropy-type" value="card">
                                                <strong>Card</strong> [A2-9TJQK][CDHS]<br>ahqs9dtc
                                            </label>
                                        </li>
                                    </ul>
                                </div>
                            </div>
                        </div>
                        <div class="form-group">
                            <div class="col-sm-2"></div>
                            <div class="col-sm-10 checkbox">
                                <label>
                                    <input type="checkbox" class="use-entropy">
                                    <span>Show entropy details</span>
                                </label>
                            </div>
                        </div>
                        <div class="form-group">
                            <div class="col-sm-2"></div>
                            <div class="col-sm-10 checkbox">
                                <label>
                                    <input type="checkbox" class="privacy-screen-toggle">
                                    <span>Hide all private info</span>
                                </label>
                            </div>
                        </div>
                        <div class="form-group">
                            <div class="col-sm-2"></div>
                            <div class="col-sm-10 checkbox">
                                <label>
                                    <input type="checkbox" class="autoCompute" checked>
                                    <span>Auto compute</span>
                                </label>
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="col-sm-2 control-label">Mnemonic Language</label>
                            <div class="col-sm-10 languages">
                                <div class="form-control no-border">
                                    <a href="#english">English</a>
                                    <a href="#japanese" title="Japanese">日本語</a>
                                    <a href="#spanish"  title="Spanish">Español</a>
                                    <a href="#chinese_simplified"  title="Chinese (Simplified)">中文(简体)</a>
                                    <a href="#chinese_traditional"  title="Chinese (Traditional)">中文(繁體)</a>
                                    <a href="#french"  title="French">Français</a>
                                    <a href="#italian"  title="Italian">Italiano</a>
                                    <a href="#korean"  title="Korean">한국어</a>
                                    <a href="#czech" title="Czech">Čeština</a>
                                    <a href="#portuguese" title="Portuguese">Português</a>
                                </div>
                            </div>
                        </div>
                        <div class="form-group text-danger PBKDF2-infos-danger hidden">
                            <label class="col-sm-2 control-label">Warning</label>
                            <div class="col-sm-10 form-control-static">
                                <span>You are using a custom number of PBKDF2 iterations. Your BIP39 seed may not show same addresses on a different software.</span>
                                <a href="#PBKDF2-notes">Read more</a>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="phrase" class="col-sm-2 control-label">BIP39 Mnemonic</label>
                            <div class="col-sm-10">
                                <textarea id="phrase" class="phrase private-data form-control" data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                            </div>
                        </div>
                        <div class="form-group">
                            <div  class="splitMnemonic hidden">
                                <label for="phrase" class="col-sm-2 control-label">BIP39 Split Mnemonic</label>
                                <div class="col-sm-10">
                                    <textarea id="phraseSplit" class="phraseSplit private-data form-control" title="Only 2 of 3 cards needed to recover." rows="3"></textarea>
                                    <p class="help-block">
                                        <span id="phraseSplitWarn" class="phraseSplitWarn"></span>
                                    </p>
                                </div>
                            </div>
                            <div class="col-sm-2">
                            </div>
                            <div class="col-sm-10">
                                <label class="control-label text-weight-normal">
                                    <input type="checkbox" class="showSplitMnemonic">
                                    Show split mnemonic cards
                                </label>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="passphrase" class="col-sm-2 control-label">BIP39 Passphrase (optional)</label>
                            <div class="col-sm-10">
                                <textarea id="passphrase" class="passphrase private-data form-control" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="seed" class="col-sm-2 control-label">BIP39 Seed</label>
                            <div class="col-sm-10">
                                <textarea id="seed" class="seed private-data form-control" data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="network-phrase" class="col-sm-2 control-label">Coin</label>
                            <div class="col-sm-10">
                                <select id="network-phrase" class="network form-control">
                                    <!-- populated by javascript -->
                                </select>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="root-key" class="col-sm-2 control-label">BIP32 Root Key</label>
                            <div class="col-sm-10">
                                <textarea id="root-key" class="root-key private-data form-control" data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                            </div>
                        </div>

                        <div class="form-group">
                            <div class="col-sm-2"></div>
                            <div class="col-sm-10">
                                <label class="control-label text-weight-normal">
                                    <input type="checkbox" class="showBip85" />
                                    Show BIP85
                                </label>
                            </div>
                        </div>

                        <div class="form-group bip85 hidden">
                            <div class="form-group text-danger">
                                <label class="col-sm-2 control-label">Warning</label>
                                <div class="col-sm-10 form-control-static">
                                    This is an advanced feature and should only be used if you understand what it does.
                                </div>
                            </div>
                            <div class="form-group">
                                <label class="col-sm-2"></label>
                                <div class="col-sm-10">
                                    <p>
                                    The value of the "BIP85 Child Key" field shown below is not used
                                    elsewhere on this page. It can be used as a new key.
                                    </p>
                                    <p>
                                    In case of the BIP39 application, you can paste it into the "BIP39 Mnemonic"
                                    field to use it as a new mnemonic.
                                    </p>
                                    <p>
                                    Please read the
                                    <a href="https://github.com/bitcoin/bips/blob/master/bip-0085.mediawiki" target="_blank">
                                        BIP85 spec
                                    </a>
                                    for more information.
                                    </p>
                                </div>
                            </div>
                            <label for="bip85-application" class="col-sm-2 control-label">BIP85 Application</label>
                            <div class="col-sm-10">
                                <select id="bip85-application" class="form-control">
                                    <option value="bip39" selected>BIP39</option>
                                    <option value="wif">WIF</option>
                                    <option value="xprv">Xprv</option>
                                    <option value="hex">Hex</option>
                                </select>
                            </div>
                        </div>

                        <div class="form-group bip85 bip85-mnemonic-language-input hidden">
                            <label for="bip85-mnemonic-language" class="col-sm-2 control-label">BIP85 Mnemonic Language</label>
                            <div class="col-sm-10 languages">
                                <select id="bip85-mnemonic-language" class="strength form-control">
                                    <option value="0" selected>English</option>
                                    <!--<option value="1">日本語</option>
                                    <option value="2">한국어</option>
                                    <option value="3">Español</option>
                                    <option value="4">中文(简体)</option>
                                    <option value="5">中文(繁體)</option>
                                    <option value="6">Français</option>
                                    <option value="7">Italiano</option>
                                    <option value="8">Čeština</option>
                                    <option value="9">Português</option>-->
                                </select>
                            </div>
                        </div>

                        <div class="form-group bip85 bip85-mnemonic-length-input hidden">
                            <label for="bip85-mnemonic-length" class="col-sm-2 control-label">BIP85 Mnemonic Length</label>
                            <div class="col-sm-10">
                                <select id="bip85-mnemonic-length" class="strength form-control">
                                    <option value="12" selected>12</option>
                                    <option value="18">18</option>
                                    <option value="24">24</option>
                                </select>
                            </div>
                        </div>

                        <div class="form-group bip85 hidden">
                            <span class="bip85-bytes-input">
                                <label for="bip85-bytes" class="col-sm-2 control-label">BIP85 Bytes</label>
                                <div class="col-sm-10">
                                    <input id="bip85-bytes" type="text" class="change form-control" value="64" />
                                </div>
                            </span>
                        </div>

                        <div class="form-group bip85 bip85-index-input hidden">
                            <label for="bip85-index" class="col-sm-2 control-label">BIP85 Index</label>
                            <div class="col-sm-10">
                                <input id="bip85-index" type="text" class="change form-control" value="0" />
                            </div>
                        </div>

                        <div class="form-group bip85 hidden">
                            <label for="phrase" class="col-sm-2 control-label">BIP85 Child Key</label>
                            <div class="col-sm-10">
                                <textarea
                                    id="bip85Field"
                                    data-show-qr
                                    class="bip85Field private-data form-control"
                                    title="BIP85 Child Key"
                                    rows="3"
                                ></textarea>
                            </div>
                        </div>

                        <div class="form-group litecoin-ltub-container hidden">
                            <label for="litecoin-use-ltub" class="col-sm-2 control-label">Prefixes</label>
                            <div class="col-sm-10 checkbox">
                                <label>
                                    <input type="checkbox" id="litecoin-use-ltub" class="litecoin-use-ltub" checked="checked">
                                    Use <code>Ltpv / Ltub</code> instead of <code>xprv / xpub</code>
                                </label>
                            </div>
                        </div>
                    </form>
                </div>
            </div>

            <hr>

            <div class="row">
                <div class="col-md-12">
                    <h2>Derivation Path</h2>
                    <ul class="derivation-type nav nav-tabs" role="tablist">
                        <li id="bip32-tab">
                            <a href="#bip32" role="tab" data-toggle="tab">BIP32</a>
                        </li>
                        <li id="bip44-tab" class="active">
                            <a href="#bip44" role="tab" data-toggle="tab">BIP44</a>
                        </li>
                        <li id="bip49-tab">
                            <a href="#bip49" role="tab" data-toggle="tab">BIP49</a>
                        </li>
                        <li id="bip84-tab">
                            <a href="#bip84" role="tab" data-toggle="tab">BIP84</a>
                        </li>
                        <li id="bip141-tab">
                            <a href="#bip141" role="tab" data-toggle="tab">BIP141</a>
                        </li>
                    </ul>
                    <div class="derivation-type tab-content">
                        <div id="bip44" class="tab-pane active">
                            <form class="form-horizontal" role="form">
                                <br>
                                <div class="col-sm-2"></div>
                                <div class="col-sm-10">
                                    <p>
                                        For more info see the
                                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki" target="_blank">BIP44 spec</a>.
                                    </p>
                                </div>
                                <div class="form-group">
                                    <label for="purpose-bip44" class="col-sm-2 control-label">
                                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#purpose" target="_blank">Purpose</a>
                                    </label>
                                    <div class="col-sm-10">
                                        <input id="purpose-bip44" type="text" class="purpose form-control" value="44" readonly>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="coin-bip44" class="col-sm-2 control-label">
                                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#registered-coin-types" target="_blank">Coin</a>
                                    </label>
                                    <div class="col-sm-10">
                                        <input id="coin-bip44" type="text" class="coin form-control" value="0" readonly>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="account-bip44" class="col-sm-2 control-label">
                                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#account" target="_blank">Account</a>
                                    </label>
                                    <div class="col-sm-10">
                                        <input id="account-bip44" type="text" class="account form-control" value="0">
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="change-bip44" class="col-sm-2 control-label">
                                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#change" target="_blank">External / Internal</a>
                                    </label>
                                    <div class="col-sm-10">
                                      <input id="change-bip44" type="text" class="change form-control" value="0">
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label class="col-sm-2 control-label">
                                    </label>
                                    <div class="col-sm-10">
                                        <p>The account extended keys can be used for importing to most BIP44 compatible wallets, such as mycelium or electrum.</p>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="account-xprv" class="col-sm-2 control-label">
                                        <span>Account Extended Private Key</span>
                                    </label>
                                    <div class="col-sm-10">
                                        <textarea id="account-xprv-bip44" type="text" class="account-xprv private-data form-control" readonly data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="account-xpub" class="col-sm-2 control-label">
                                        <span>Account Extended Public Key</span>
                                    </label>
                                    <div class="col-sm-10">
                                        <textarea id="account-xpub-bip44" type="text" class="account-xpub form-control" readonly data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label class="col-sm-2 control-label">
                                    </label>
                                    <div class="col-sm-10">
                                        <p>The BIP32 derivation path and extended keys are the basis for the derived addresses.</p>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="bip44-path" class="col-sm-2 control-label">BIP32 Derivation Path</label>
                                    <div class="col-sm-10">
                                        <input id="bip44-path" type="text" class="path form-control" value="m/44'/0'/0'/0" readonly="readonly">
                                    </div>
                                </div>
                            </form>
                        </div>
                        <div id="bip32" class="tab-pane">
                            <form class="form-horizontal" role="form">
                                <br>
                                <div class="col-sm-2"></div>
                                <div class="col-sm-10">
                                    <p>
                                        For more info see the
                                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki" target="_blank">BIP32 spec</a>
                                    </p>
                                </div>
                                <div class="form-group">
                                    <label for="bip32-client" class="col-sm-2 control-label">Client</label>
                                    <div class="col-sm-10">
                                        <select id="bip32-client" class="client form-control">
                                            <option value="custom">Custom derivation path</option>
                                            <!-- populated by javascript -->
                                        </select>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="bip32-path" class="col-sm-2 control-label">BIP32 Derivation Path</label>
                                    <div class="col-sm-10">
                                        <input id="bip32-path" type="text" class="path form-control" value="m/0">
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="core-path" class="col-sm-2 control-label">Bitcoin Core</label>
                                    <div class="col-sm-10">
                                        <p class="form-control no-border">
                                        Use path <code>m/0'/0'</code> with hardened addresses.
                                        </p>
                                        <p class="form-control no-border">
                                            For more info see the
                                            <a href="https://github.com/bitcoin/bitcoin/pull/8035" target="_blank">Bitcoin Core BIP32 implementation</a>
                                        </p>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label for="core-path" class="col-sm-2 control-label">Multibit</label>
                                    <div class="col-sm-10">
                                        <p class="form-control no-border">
                                            <span>Use path <code>m/0'/0</code>.</span>
                                            <span>For change addresses use path <code>m/0'/1</code>.</span>
                                        </p>
                                        <p class="form-control no-border">
                                            <span>For more info see</span>
                                            <a href="https://multibit.org/" target="_blank">MultiBit HD</a>
                                        </p>
                                    </div>
                                </div>
                                <div class="form-group">
                                    <label class="col-sm-2 control-label">Block Explorers</label>
                                    <div class="col-sm-10">
                                        <p class="form-control no-border">
                                            <span>Use path <code>m/44'/0'/0'</code>.</span>
                                            <span>Only enter the <code>xpub</code> extended key into block explorer search fields, never the <code>xprv</code> key.</span>
                                        </p>
                                        <p class="form-control no-border">
                                            <span>Can be used with</span>:
                                            <a href="https://blockchain.info/" target="_blank">blockchain.info</a>
                                        </p>
                                    </div>
                                </div>
                            </form>
                        </div>
                        <div id="bip49" class="tab-pane">
                            <form class="form-horizontal" role="form">
                                <br>
                                <div class="unavailable hidden">
                                    <div class="form-group">
                                        <div class="col-sm-2"></div>
                                        <div class="col-sm-10">
                                            <p>BIP49 is unavailable for this coin.</p>
                                        </div>
                                    </div>
                                </div>
                                <div class="available">
                                    <div class="col-sm-2"></div>
                                    <div class="col-sm-10">
                                        <p>
                                            For more info see the
                                            <a href="https://github.com/bitcoin/bips/blob/master/bip-0049.mediawiki" target="_blank">BIP49 spec</a>.
                                        </p>
                                    </div>
                                    <div class="form-group">
                                        <label for="purpose-bip49" class="col-sm-2 control-label">
                                            <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#purpose" target="_blank">Purpose</a>
                                        </label>
                                        <div class="col-sm-10">
                                            <input id="purpose-bip49" type="text" class="purpose form-control" value="49" readonly>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="coin-bip49" class="col-sm-2 control-label">
                                            <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#registered-coin-types" target="_blank">Coin</a>
                                        </label>
                                        <div class="col-sm-10">
                                            <input id="coin-bip49" type="text" class="coin form-control" value="0" readonly>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="account-bip49" class="col-sm-2 control-label">
                                            <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#account" target="_blank">Account</a>
                                        </label>
                                        <div class="col-sm-10">
                                            <input id="account-bip49" type="text" class="account form-control" value="0">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="change-bip49" class="col-sm-2 control-label">
                                            <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki#change" target="_blank">External / Internal</a>
                                        </label>
                                        <div class="col-sm-10">
                                            <input id="change-bip49" type="text" class="change form-control" value="0">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label class="col-sm-2 control-label">
                                        </label>
                                        <div class="col-sm-10">
                                            <p>The account extended keys can be used for importing to most BIP49 compatible wallets.</p>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="account-xprv" class="col-sm-2 control-label">
                                            <span>Account Extended Private Key</span>
                                        </label>
                                        <div class="col-sm-10">
                                            <textarea id="account-xprv-bip49" type="text" class="account-xprv private-data form-control" readonly data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="account-xpub" class="col-sm-2 control-label">
                                            <span>Account Extended Public Key</span>
                                        </label>
                                        <div class="col-sm-10">
                                            <textarea id="account-xpub-bip49" type="text" class="account-xpub form-control" readonly data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label class="col-sm-2 control-label">
                                        </label>
                                        <div class="col-sm-10">
                                            <p>The BIP32 derivation path and extended keys are the basis for the derived addresses.</p>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="bip49-path" class="col-sm-2 control-label">BIP32 Derivation Path</label>
                                        <div class="col-sm-10">
                                            <input id="bip49-path" type="text" class="path form-control" value="m/49'/0'/0'/0" readonly="readonly">
                                        </div>
                                    </div>
                                </div>
                            </form>
                        </div>
                        <div id="bip141" class="tab-pane">
                            <form class="form-horizontal" role="form">
                                <br>
                                <div class="unavailable hidden">
                                    <div class="form-group">
                                        <div class="col-sm-2"></div>
                                        <div class="col-sm-10">
                                            <p>BIP141 is unavailable for this coin.</p>
                                        </div>
                                    </div>
                                </div>
                                <div class="available">
                                    <div class="col-sm-2"></div>
                                    <div class="col-sm-10">
                                        <p>
                                            For more info see the
                                            <a href="https://github.com/bitcoin/bips/blob/master/bip-0141.mediawiki" target="_blank">BIP141 spec</a>
                                        </p>
                                    </div>
                                    <div class="form-group">
                                        <label for="bip141-path" class="col-sm-2 control-label">BIP32 Derivation Path</label>
                                        <div class="col-sm-10">
                                            <input id="bip141-path" type="text" class="bip141-path form-control" value="m/0">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label class="col-sm-2 control-label">Script Semantics</label>
                                        <div class="col-sm-10">
                                            <select class="form-control bip141-semantics">
                                                <option value="p2wpkh">P2WPKH</option>
                                                <option value="p2wpkh-p2sh" selected>P2WPKH nested in P2SH</option>
                                                <option value="p2wsh">P2WSH (1-of-1 multisig)</option>
                                                <option value="p2wsh-p2sh">P2WSH nested in P2SH (1-of-1 multisig)</option>
                                            </select>
                                        </div>
                                    </div>
                                </div>
                            </form>
                        </div>
                        <div id="bip84" class="tab-pane">
                            <form class="form-horizontal" role="form">
                                <br>
                                <div class="unavailable hidden">
                                    <div class="form-group">
                                        <div class="col-sm-2"></div>
                                        <div class="col-sm-10">
                                            <p>BIP84 is unavailable for this coin.</p>
                                        </div>
                                    </div>
                                </div>
                                <div class="available">
                                    <div class="col-sm-2"></div>
                                    <div class="col-sm-10">
                                        <p>
                                            For more info see the
                                            <a href="https://github.com/bitcoin/bips/blob/master/bip-0084.mediawiki" target="_blank">BIP84 spec</a>.
                                        </p>
                                    </div>
                                    <div class="form-group">
                                        <label for="purpose-bip84" class="col-sm-2 control-label">
                                            Purpose
                                        </label>
                                        <div class="col-sm-10">
                                            <input id="purpose-bip84" type="text" class="purpose form-control" value="84" readonly>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="coin-bip84" class="col-sm-2 control-label">
                                            Coin
                                        </label>
                                        <div class="col-sm-10">
                                            <input id="coin-bip84" type="text" class="coin form-control" value="0" readonly>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="account-bip84" class="col-sm-2 control-label">
                                            Account
                                        </label>
                                        <div class="col-sm-10">
                                            <input id="account-bip84" type="text" class="account form-control" value="0">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="change-bip84" class="col-sm-2 control-label">
                                            External / Internal
                                        </label>
                                        <div class="col-sm-10">
                                            <input id="change-bip84" type="text" class="change form-control" value="0">
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label class="col-sm-2 control-label">
                                        </label>
                                        <div class="col-sm-10">
                                            <p>The account extended keys can be used for importing to most BIP84 compatible wallets.</p>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="account-xprv" class="col-sm-2 control-label">
                                            <span>Account Extended Private Key</span>
                                        </label>
                                        <div class="col-sm-10">
                                            <textarea id="account-xprv-bip84" type="text" class="account-xprv private-data form-control" readonly data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="account-xpub" class="col-sm-2 control-label">
                                            <span>Account Extended Public Key</span>
                                        </label>
                                        <div class="col-sm-10">
                                            <textarea id="account-xpub-bip84" type="text" class="account-xpub form-control" readonly data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label class="col-sm-2 control-label">
                                        </label>
                                        <div class="col-sm-10">
                                            <p>The BIP32 derivation path and extended keys are the basis for the derived addresses.</p>
                                        </div>
                                    </div>
                                    <div class="form-group">
                                        <label for="bip84-path" class="col-sm-2 control-label">BIP32 Derivation Path</label>
                                        <div class="col-sm-10">
                                            <input id="bip84-path" type="text" class="path form-control" value="m/84'/0'/0'/0" readonly="readonly">
                                        </div>
                                    </div>
                                </div>
                            </form>
                        </div>
                    </div>
                    <form class="form-horizontal" role="form">
                        <div class="form-group">
                            <label for="extended-priv-key" class="col-sm-2 control-label">BIP32 Extended Private Key</label>
                            <div class="col-sm-10">
                                <textarea id="extended-priv-key" class="extended-priv-key private-data form-control" readonly="readonly" data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="extended-pub-key" class="col-sm-2 control-label">BIP32 Extended Public Key</label>
                            <div class="col-sm-10">
                                <textarea id="extended-pub-key" class="extended-pub-key form-control" readonly="readonly" data-show-qr autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                            </div>
                        </div>
                    </form>
                </div>
            </div>

            <hr>

            <div class="row">
                <div class="col-md-12">
                    <h2>Derived Addresses</h2>
                    <p>Note these addresses are derived from the BIP32 Extended Key</p>
                </div>
                <div class="col-md-12 bch-addr-type-container hidden">
                    <div class="radio">
                        <label>
                            <input type="radio" value="cashaddr" name="bch-addr-type" class="use-bch-cashaddr-addresses" checked="checked">
                            <span>Use CashAddr addresses for Bitcoin Cash (ie starting with 'q' instead of '1')</span>
                        </label>
                    </div>
                    <div class="radio">
                        <label>
                            <input type="radio" value="bitpay" name="bch-addr-type" class="use-bch-bitpay-addresses">
                            <span>Use BitPay-style addresses for Bitcoin Cash (ie starting with 'C' instead of '1')</span>
                        </label>
                    </div>
                    <div class="radio">
                        <label>
                            <input type="radio" value="legacy" name="bch-addr-type" class="use-bch-legacy-addresses">
                            <span>Use legacy addresses for Bitcoin Cash (ie starting with '1')</span>
                        </label>
                    </div>
                </div>
                <div class="col-md-12">
                    <div class="checkbox">
                        <label>
                            <input type="checkbox" class="use-bip38">
                            <span>Encrypt private keys using BIP38 and this password:</span>
                        </label>
                        <input class="bip38-password private-data" autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false">
                        <span>Enabling BIP38 means each key will take several minutes to generate.</span>
                    </div>
                </div>
                <div class="col-md-12">
                    <div class="checkbox">
                        <label>
                            <input class="hardened-addresses" type="checkbox">
                            <span>Use hardened addresses</span>
                        </label>
                    </div>
                </div>
                <ul class="addresses-type nav nav-tabs" role="tablist">
                    <li id="table-tab" class="active">
                        <a href="#table" role="tab" data-toggle="tab">Table</a>
                    </li>
                    <li id="csv-tab">
                        <a href="#csv" role="tab" data-toggle="tab">CSV</a>
                    </li>
                </ul>
                <div class="addresses-type tab-content">
                    <div id="table" class="tab-pane active">
                        <div class="col-md-12">
                            <table class="table table-striped">
                                <thead>
                                    <th>
                                        <div class="input-group">
                                            <span>Path</span>&nbsp;&nbsp;
                                            <button class="index-toggle">Toggle</button>
                                        </div>
                                    </th>
                                    <th>
                                        <div class="input-group">
                                            <span>Address</span>&nbsp;&nbsp;
                                            <button class="address-toggle">Toggle</button>
                                        </div>
                                    </th>
                                    <th>
                                        <div class="input-group">
                                            <span>Public Key</span>&nbsp;&nbsp;
                                            <button class="public-key-toggle">Toggle</button>
                                        </div>
                                    </th>
                                    <th>
                                        <div class="input-group">
                                            <span>Private Key</span>&nbsp;&nbsp;
                                            <button class="private-key-toggle">Toggle</button>
                                        </div>
                                    </th>
                                </thead>
                                <tbody class="addresses monospace">
                                    <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
                                    <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
                                    <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
                                    <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
                                    <tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    <div id="csv" class="tab-pane">
                        <div class="col-md-12">
                            <textarea class="csv form-control" rows="25" readonly autocomplete="off" autocorrect="off" autocapitalize="off" spellcheck="false"></textarea>
                        </div>
                    </div>
                </div>
            </div>
            <span>Show</span>
            <input type="number" class="rows-to-add" value="20">
            <button class="more">more rows</button>
            <span>starting from index</span>
            <input type="number" class="more-rows-start-index">
            <span>(leave blank to generate from next index)</span>

            <hr>

            <div class="row">
                <div class="col-md-12">
                    <h2>More info</h2>
                    <h3>BIP39 <span class="small">Mnemonic code for generating deterministic keys</span></h3>
                    <p>
                        Read more at the
                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki">official BIP39 spec</a>
                    </p>
                    <h3>BIP32 <span class="small">Hierarchical Deterministic Wallets</span></h3>
                    <p>
                        Read more at the
                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0032.mediawiki" target="_blank">official BIP32 spec</a>
                    </p>
                    <p>
                        See the demo at
                        <a href="http://bip32.org/" target="_blank">bip32.org</a>
                    </p>
                    <h3>BIP44 <span class="small">Multi-Account Hierarchy for Deterministic Wallets</span></h3>
                    <p>
                        Read more at the
                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0044.mediawiki" target="_blank">official BIP44 spec</a>
                    </p>
                    <h3>BIP49 <span class="small">Derivation scheme for P2WPKH-nested-in-P2SH based accounts</span></h3>
                    <p>
                        Read more at the
                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0049.mediawiki" target="_blank">official BIP49 spec</a>
                    </p>
                    <h3>BIP85 <span class="small">Deterministic Entropy From BIP32 Keychains</span></h3>
                    <p>
                        Read more at the
                        <a href="https://github.com/bitcoin/bips/blob/master/bip-0085.mediawiki" target="_blank">official BIP85 spec</a>
                    </p>
                    <h3 id="entropy-notes">Entropy</h3>
                    <p>
                        <span>Entropy values should not include the BIP39 checksum. This is automatically added by the tool.</span>
                    </p>
                    <p>
                        <span>
                            Entropy values must be sourced from a
                            <a href="https://en.wikipedia.org/wiki/Random_number_generation" target="_blank">strong source of randomness</a>.
                        </span>
                        <span>This means flipping a fair coin, rolling a fair dice, noise measurements etc.</span>
                        <span>
                            Do <strong>NOT</strong> use phrases from books, lyrics from songs, your birthday or street address,
                            keyboard mashing, or anything you <i>think</i> is random, because chances are overwhelming it isn't
                            random enough for the needs of this tool.
                        </span>
                    </p>
                    <p>
                        <strong><span>Do not store entropy.</span></strong>
                    </p>
                    <p>
                        <span>Storing entropy (such as keeping a deck of cards in a specific shuffled order) is unreliable compared to storing a mnemonic.</span>
                        <span>Instead of storing entropy, store the mnemonic generated from the entropy.</span>
                        <span><a href="https://en.wikipedia.org/wiki/Steganography#Physical" target="_blank">Steganography</a> may be beneficial when storing the mnemonic.</span>
                    </p>
                    <p>
                        <span>
                            The random mnemonic generator on this page uses a
                            <a href="https://developer.mozilla.org/en-US/docs/Web/API/RandomSource/getRandomValues" target="_blank">cryptographically secure random number generator</a>.
                        </span>
                        <span>The built in random generator can generally be trusted more than your own intuition about randomness.</span>
                        <span>If cryptographic randomness isn't available in your browser, this page will show a warning and the generate button will not work.</span>
                        <span>In that case you might choose to use your own source of entropy.</span>
                    </p>
                    <p>
                        <a href="https://bitcointalk.org/index.php?topic=311000.msg3345309#msg3345309" target="_blank">You are not a good source of entropy.</a>
                    </p>
                    <p>
                        <span>Card entropy has been implemented assuming cards are replaced, not drawn one after another.</span>
                        <span>A full deck with replacement generates 232 bits of entropy (21 words). A full deck without replacement generates 225 bits of entropy (21 words).</span>
                        <span>Card entropy changed significantly from v0.4.3 to v0.5.0. The old version can be accessed at
                            <a href="https://github.com/iancoleman/bip39/releases/tag/0.4.3">
                                https://github.com/iancoleman/bip39/releases/tag/0.4.3
                            </a>
                            or
                            <a href="https://web.archive.org/web/20201018232020/https://iancoleman.io/bip39/">
                                https://web.archive.org/web/20201018232020/https://iancoleman.io/bip39/
                            </a>
                        </span>
                    </p>
                    <h3 id="PBKDF2-notes">PBKDF2</h3>
                    <p><a href="https://learnmeabitcoin.com/technical/mnemonic#pbkdf2---password-based-key-derivation-function-2   " target="_blank">What is PBKDF2 (Password Based Key Derivation Function 2) ?</a></p>
                    <p><span>Please refer to this <a href="https://en.wikipedia.org/wiki/PBKDF2" target="_blank">wikipedia article</a> for more detail.
                    <span>Mail about PBKDF2 security <a href="https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2016-July/012902.html" target="_blank">here</a>.</p>
                    <p>Wallet software that implement BIP39 only use 2048 iterations as a norm. Increasing this parameter will increase security against brute force attack, but you will need to store this new parameter. However, as long as you back up your BIP39 seed there will not be risk to lost your fund. To access them with custom PBKDF2 iterations, use this file (or <a href="https://stuff.birkenstab.de/pbkdf2/" target="_blank">other</a>) to compute your targeted BIP39 seed.</p>
                    <p>Using less than 2048 PBKDF2 iterations is insecure without strong optional BIP39 Passphrase.</p>
                    <h3>License</h3>
                    <p>
                    <span>Please refer to <a href="https://github.com/iancoleman/bip39/blob/master/LICENSE" target="_blank">the software license</a> for more detail.
                    </span>
                    </p>
                    <p>The software is provided "as is", without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages or other liability, whether in an action of contract, tort or otherwise, arising from, out of or in connection with the software or the use or other dealings in the software.</p>
                </div>
            </div>

            <hr>

            <div class="row">
                <div class="col-md-12">
                    <h2>Alternative Tools</h2>
                    <p>This tool is interoperable with any BIP39 wallet.</p>
                    <p>Some similar tools to this one (ie not consumer wallets) are</p>
                    <p>
                        <a href="https://bip32jp.github.io/english/">
                            https://bip32jp.github.io/english/
                        </a>
                    </p>
                </div>
            </div>

            <hr>

            <div class="row">
                <div class="col-md-12">

                    <h2>Offline Usage</h2>

                    <p>
                    You can use this tool without having to be online.
                    </p>
                    <p>
                    In your browser, select file save-as, and save this page
                    as a file.
                    </p>
                    <p>
                    Double-click that file to open it in a browser
                    on any offline computer.
                    </p>
                    <p>
                    <span>Alternatively, download the file from the latest GitHub release</span>
                    -
                    <a href="https://github.com/iancoleman/bip39/releases/latest/">https://github.com/iancoleman/bip39/releases/latest/</a>
                    </p>

                </div>
            </div>

            <hr>

            <div class="row">
                <div class="col-md-12">

                    <h2>This project is 100% open-source code</h2>

                    <p>
                        <span>Get the source code from the repository</span>
                        -
                        <a href="https://github.com/iancoleman/bip39" target="_blank">
                            https://github.com/iancoleman/bip39
                        </a>
                    </p>

                    <h3>Libraries</h3>

                    <p>
                        <span>BitcoinJS - </span>
                        <a href="https://github.com/bitcoinjs/bitcoinjs-lib" target="_blank">
                            https://github.com/bitcoinjs/bitcoinjs-lib
                        </a>
                    </p>

                    <p>
                        <span>jsBIP39 - </span>
                        <a href="https://github.com/iancoleman/jsbip39" target="_blank">
                            https://github.com/iancoleman/jsbip39
                        </a>
                    </p>

                    <p>
                        <span>sjcl - </span>
                        <a href="https://github.com/bitwiseshiftleft/sjcl" target="_blank">
                            https://github.com/bitwiseshiftleft/sjcl
                        </a>
                    </p>

                    <p>
                        <span>jQuery - </span>
                        <a href="https://jquery.com/" target="_blank">
                            https://jquery.com/
                        </a>
                    </p>

                    <p>
                        <span>Twitter Bootstrap - </span>
                        <a href="http://getbootstrap.com/" target="_blank">
                            http://getbootstrap.com/
                        </a>
                    </p>

                </div>
            </div>

        </div>

        <div class="qr-container hidden">
            <div class="qr-hint bg-primary hidden">Click field to hide QR</div>
            <div class="qr-hint bg-primary">Click field to show QR</div>
            <div class="qr-hider hidden">
                <div class="qr-image"></div>
                <div class="qr-warning bg-primary">Caution: Scanner may keep history</div>
            </div>
        </div>

        <div class="feedback-container">
            <div class="feedback">Loading...</div>
        </div>

        <script type="text/template" id="address-row-template">
            <tr>
                <td class="index"><span></span></td>
                <td class="address"><span data-show-qr></span></td>
                <td class="pubkey"><span data-show-qr></span></td>
                <td class="privkey private-data"><span data-show-qr></span></td>
            </tr>
        </script>
        <script src="js/jquery-3.2.1.js"></script>
        <script src="js/bootstrap.js"></script>
        <script src="js/bip39-libs.js"></script>
        <script src="js/bitcoinjs-extensions.js"></script>
        <script src="js/segwit-parameters.js"></script>
        <script src="js/ripple-util.js"></script>
        <script src="js/jingtum-util.js"></script>
        <script src="js/casinocoin-util.js"></script>
        <script src="js/cosmos-util.js"></script>
        <script src="js/eos-util.js"></script>
        <script src="js/fio-util.js"></script>
        <script src="js/xwc-util.js"></script>
        <script src="js/sjcl-bip39.js"></script>
        <script src="js/wordlist_english.js"></script>
        <script src="js/wordlist_japanese.js"></script>
        <script src="js/wordlist_spanish.js"></script>
        <script src="js/wordlist_chinese_simplified.js"></script>
        <script src="js/wordlist_chinese_traditional.js"></script>
        <script src="js/wordlist_french.js"></script>
        <script src="js/wordlist_italian.js"></script>
        <script src="js/wordlist_korean.js"></script>
        <script src="js/wordlist_czech.js"></script>
        <script src="js/wordlist_portuguese.js"></script>
        <script src="js/jsbip39.js"></script>
        <script src="js/entropy.js"></script>
        <script src="js/index.js"></script>
    </body>
</html>
