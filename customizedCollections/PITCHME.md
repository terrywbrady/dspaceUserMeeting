### Talk: Building Customized Collections in DSpace

Terry Brady, Suzanne Chase, Salwa Ismail, Leah Prescott

Georgetown University Library

Georgetown Law Library

![](https://www.library.georgetown.edu/sites/default/files/library-logo.png)
![](https://repository.library.georgetown.edu/themes/law-lib//images/gull_logo.jpg)


+++

### DigitalGeorgetown Overview

* 536,000 Items
  * Largest or 2nd Largest DSpace Instance by Item Count
* Replaced Several Legacy Databases at the University
  * Art History Database of 150,000 items restricted to the Georgetown Community
  * 350,000 Bioethics Citations

+++

### Overview

* Why Customize? Terry Brady
* Collection Customization - Leah Prescott
* Viewer Integration - Suzanne Chase

---

### Why To Customize Your Repository (Salwa)

* Customization Goals 
* Repository Branding
* Community Themes
* LMS Integration
* Theme Simplification

+++

### Customization Goals

* Branding
* Stakeholder Buy-In
* Improved Usability

+++

### Repository Branding

* https://repository.library.georgetown.edu
  * Branding Logos
  * AddThis Menu Integration
* DigitalGeorgetown Portal
  * http://www.library.georgetown.edu/digitalgeorgetown
  

+++

### 5 Major Community Themes

* [Default Theme](https://repository.library.georgetown.edu/)
* [IR Theme](https://repository.library.georgetown.edu/handle/10822/1)
* [Bioethics Library Theme](https://repository.library.georgetown.edu/handle/10822/503786)
* [Law Library Theme](https://repository.library.georgetown.edu/handle/10822/555527)
* [Special Collections Themes](https://repository.library.georgetown.edu/handle/10822/1042291)

+++

### Community Themes

* Set default logo, header, footer
* Set default microtag behavior (SEO)
* Set default Google Scholar metadata

+++

### xmlui.xconf

```
<theme name="Bioethics Research Library" handle="10822/503786" path="bioethics/" /> 
<theme name="SpecialCollections" handle="10822/7" path="misc/" /> 
<theme name="ITEL" handle="10822/710899" path="misc/" /> 
<theme name="GUPUB" handle="10822/549395" path="misc/" /> 
<theme name="PREVIEW" handle="10822/761364" path="misc/" /> 
<theme name="IR" handle="10822/1" path="ir/" /> 
<theme name="Law Library" handle="10822/555527" path="law-lib/" />
<theme name="GU Base Theme" regex=".*" path="Mirage2/" /> 
```
@[8](Default Theme)
@[1](Bioethics Theme)
@[2-5](Special Collections "Misc" Theme)
@[6](IR Theme)
@[7](Law Theme)

+++

### Sample Custom Theme
```
<xsl:import href="../../Mirage2/xsl/theme.xsl"/>
<xsl:output indent="yes"/>
<xsl:variable name="header-logo-link">http://bioethics.georgetown.edu</xsl:variable>
<xsl:variable name="header-logo-link-lang">Bioethics Research Library Website</xsl:variable>
<xsl:variable name="header-logo" select="concat($theme-path,'/images/bioethics-logo.png')"/>
<xsl:variable name="header-logo-alt">Bioethics Research Library Logo</xsl:variable>
<xsl:variable name="MICROTAG"/>
```
@[1](Theme is derived from the default Mirage2 theme)
@[3-6](Custom Logo and Link via XSL Variables)
@[7](Disable Creation of Microtags for this Community)

+++

### Custom Footer
```
<xsl:template name="guFooterText">
    <xsl:text>&#xA9;2009&#x2014;</xsl:text>
    <xsl:call-template name="getCopyrightYear"/>
    <xsl:text> Bioethics Research Library</xsl:text>
    <br/> 
    <xsl:text>Box 571212 Washington DC 20057-1212</xsl:text>
    <br/>
    <xsl:text>202.687.3885</xsl:text>
</xsl:template>
```
@[1-9](Theme-specific footer - xsl template override)

+++

### LMS Integration

[DigitalGeorgetown MashUp in Blackboard](https://github.com/Georgetown-University-Libraries/georgetown-university-libraries.github.io/wiki/Linking-Digital-Resources-to-the-University-Learning-Management-System)

+++

### Theme Simplification

* We used to provide themes with significant visual variation
* New themes have less visual differentiation since the adoption of the Mirage2 responsive theme
* Focus on impactful, collection-specific customizations

+++?image=https://cloud.githubusercontent.com/assets/1111057/8435057/1798071c-1f04-11e5-921b-9539ce16117d.png
+++?image=customizedCollections/covey.png
+++?image=https://cloud.githubusercontent.com/assets/1111057/8435523/815fb062-1f06-11e5-891d-9a3e4a96fb5a.png
+++?image=customizedCollections/mclaughlin.png
+++?image=customizedCollections/krogh.png
+++?image=customizedCollections/kroghNew.png

+++

### New Customization Example: Ambassadors Portal

* [Ambassadors Portal (Test Server)](https://repository-test.library.georgetown.edu/handle/10822/1043019)
* Custom Facets to Facilitate Discovery
* Item Summary Page links to Custom Facets
* External finding aid link

---

### Collection Theme Variations (Leah)
* 51 Theme Variations 
  * Logos
  * Custom Item Summary Pages
* 14 Custom Facets

+++

### Collection Theme Goals

* Make navigation more intuitive
* Improve buy-in with stake-holders

+++
### Identify Specific Collections by Handle

```
<xsl:variable name="IS_ANGELICA" select="key('myancestor','10822/559388')"/>
<xsl:variable name="IS_KROGH" select="key('myancestor','10822/549457')"/>
<xsl:variable name="IS_KROGH_VID" select="key('myancestor','10822/552494')"/>
<xsl:variable name="IS_ART" select="key('myancestor','10822/549413')"/>
<xsl:variable name="IS_COVEY" select="key('myancestor','10822/761365')"/>
<xsl:variable name="IS_ENVISION" select="key('myancestor','10822/549431')"/>
<xsl:variable name="IS_ITEL" select="key('myancestor','10822/710899')"/>
<xsl:variable name="IS_GUPUB" select="key('myancestor','10822/549395')"/>
<xsl:variable name="IS_PRESS" select="key('myancestor','10822/551429')"/>
<xsl:variable name="IS_RAREBK" select="key('myancestor','10822/549455')"/>
<xsl:variable name="IS_SCCAT" select="key('myancestor','10822/551505')"/>
<xsl:variable name="IS_PROJRE" select="key('myancestor','10822/1042291')"/>
```
@[1-12](Use xsl variables for small theme variations)

+++ 

### Set Microtags for Special Collections

```    
<xsl:variable name="MICROTAG">
  <xsl:choose>
    <xsl:when test="$IS_ANGELICA"/>
    <xsl:when test="$IS_GUPUB or $IS_SCCAT or $IS_RAREBK">
      <xsl:value-of select="$SCH_BOOK"/>
    </xsl:when>
    <xsl:when test="$IS_KROGH_VID or $IS_ITEL">
      <xsl:value-of select="$SCH_VID"/>
    </xsl:when>
    <xsl:when test="$IS_ENVISION">
      <xsl:value-of select="$SCH_PHOTO"/>
    </xsl:when>
    <xsl:when test="$IS_ART">
      <xsl:value-of select="$SCH_VISART"/>
    </xsl:when>
    <xsl:otherwise>
      <xsl:value-of select="$SCH_DEFAULT"/>
    </xsl:otherwise>
  </xsl:choose>
</xsl:variable>
```    
@[3](Set Microtag Properties by collection)
@[4-6](Set Microtag Properties by collection)
@[7-9](Set Microtag Properties by collection)
@[10-12](Set Microtag Properties by collection)
@[13-15](Set Microtag Properties by collection)
@[16-18](Set Default Microtag Properties)

+++

### Collection Logos
```
<xsl:template match="dri:div[@n='community-home' or @n='collection-home']/dri:head" priority="3">
  <xsl:choose>
    <xsl:when test="$IS_COVEY">
      <xsl:call-template name="showLogo">
        <xsl:with-param name="header-logo" select="concat($theme-path,'/images/covey.jpg')"/>
        <xsl:with-param name="header-logo-alt">'Fish,' Copyright Rosemary Covey.</xsl:with-param>
      </xsl:call-template>
    </xsl:when>
    <xsl:when test="$IS_KROGH">
      <xsl:call-template name="showLogo">
        <xsl:with-param name="header-logo" select="concat($theme-path,'/images/krogh-logo.png')"/>
        <xsl:with-param name="header-logo-alt">Dean Peter Krogh Foreign Affairs Digital Archives Logo</xsl:with-param>
      </xsl:call-template>
    </xsl:when>
    <xsl:when test="$IS_ENVISION">
      <xsl:call-template name="showLogo">
        <xsl:with-param name="header-logo" select="concat($theme-path,'/images/envision-church-logo.png')"/>
        <xsl:with-param name="header-logo-alt">Envision Church Logo</xsl:with-param>
        <xsl:with-param name="header-logo-link-lang">Envision Church Website</xsl:with-param>
        <xsl:with-param name="header-logo-link">http://www.library.georgetown.edu/partners/envision-church</xsl:with-param>
      </xsl:call-template>
    </xsl:when>
```
@[3-8](Set Collection Logo)
@[9-14](Set Collection Logo)
@[15-22](Set Collection Logo/Link Target)

+++

### Customized Item Summary Page

* Custom help links
* Fields to list
* Custom field headers
* Hyperlinked Terms
* Hyperlinked to Custom Facet

+++

### Customized Item Summary Page

* [Default Item Summary Page](https://repository.library.georgetown.edu/handle/10822/1043018)
* [Summary Page for Art Item](https://repository.library.georgetown.edu/handle/10822/1040563)

+++

### Customize Field Labels by Collection
```xml 
<xsl:variable name="H_AUTHOR">
  <xsl:choose>
    <xsl:when test="$IS_PROJRE">Person Interviewed</xsl:when>
    <xsl:when test="$IS_ANGELICA">Artist</xsl:when>
    <xsl:when test="$IS_COVEY">Artist</xsl:when>
    <xsl:when test="$IS_KROGH">Moderator</xsl:when>
    <xsl:when test="$IS_ITEL">Creator</xsl:when>
    <xsl:when test="$IS_AMB">Ambassador</xsl:when>
    <xsl:otherwise>Author</xsl:otherwise>
  </xsl:choose>
</xsl:variable>
```
@[3](Treat creator/author as "Interviewee")
@[4-5](Treat creator/author as "Artist")
@[6](Treat creator/author as "Moderator")
@[7](Treat creator/author as "Creator") 
@[8](Treat creator/author as "Ambassador")
@[9](Default to "Author")
+++
Add Custom Field for a Collection
```
<xsl:template name="itemSummaryView-DIM-custom">
  <xsl:choose>
    <xsl:when test="$IS_COVEY">
      <xsl:if test="dim:field[@element='identifier' and @qualifier='other' and descendant::text()]">
        <div class="simple-item-view-uri item-page-field-wrapper table">
          <h5>Accession Number</h5>
          <span>
            <xsl:for-each select="dim:field[@element='identifier' and @qualifier='other']">
              <xsl:value-of select="text()"/>
              <xsl:if test="count(following-sibling::dim:field[@element='identifier' and @qualifier='other']) != 0">
                <xsl:text>; </xsl:text>
              </xsl:if>
            </xsl:for-each>
          </span>
        </div>
      </xsl:if>
    </xsl:when>
    <!-- ... more cases -->
  </xsl:choose>
</xsl:template> 

@[3](Test for specific collection)
@[4](Look for specific metadata field)
@[9-13](Display all values discovered) 
```
+++

### Customize Link Target for a Summary Page Field
```
<xsl:variable name="FILTER_SUBJECT">
  <xsl:choose>
    <xsl:when test="$IS_COVEY">/handle/10822/761365/discover?field=keywords&amp;filtertype=keywords&amp;filter_relational_operator=equals&amp;filter=</xsl:when>
    <xsl:otherwise>
      <xsl:value-of select="$DFILTER_SUBJECT"/>
    </xsl:otherwise>
 </xsl:choose>
</xsl:variable>
```
@[1-8](Customize Link Target for a Summary Page Field)
@[3](Hyperlink to a facet within a collection)

+++

### Special Cases 

* Item Description as Markdown
* Description of External Resources

+++

### Item Description as Markdown
 
The following collection supports item descriptions written in Markdown.

The collection theme links out to a custom glossary.

* [DC Historic Preservation Law](https://repository.library.georgetown.edu/handle/10822/1043014)

+++

### External Resources

* [Court Records and Briefs at the Internet Archive](https://repository.library.georgetown.edu/handle/10822/1043058) 

+++

### Customized Collection Page / Facets

* [Default Collection Page - IR](https://repository.library.georgetown.edu/handle/10822/1)
* [DC Historic Preservation Law](https://repository.library.georgetown.edu/handle/10822/761426)
* [Art Collection - Angelica](https://repository.library.georgetown.edu/handle/10822/559388)

---

### Repository Integration (Suzanne Chase)

* Integrated Viewers
* Discovery (Summon)
* Other Enhancements

+++

### Integrated Viewers

* [Document Viewer - FlexPaper](https://repository.library.georgetown.edu/bookview/10822/001/042/1042290/2/index.html)
* Sharestream Viewer
  * [Publicly available video](https://repository.library.georgetown.edu/handle/10822/552590)
  * [Publicly available video with still](https://repository.library.georgetown.edu/handle/10822/1044059)
  * [Limited access video](https://repository.library.georgetown.edu/handle/10822/710122)
  * [Audio Archives](https://repository.library.georgetown.edu/handle/10822/712415)
* [ArchivesSpace Integration](https://repository.library.georgetown.edu/handle/10822/1042600)

+++

### Discovery Integration

* Did troubleshooting with Summon to use OAI harvester
* Defined a strategy to identify full text / non full text
* [DG Finding Aid Example in Summon]( http://gt.summon.serialssolutions.com/#!/search?ho=t&l=en&bookMark=ePnHCXMw42LgTQStzc4rAe_hSuFkkAevzlbwAOaPPCsFZ2CI5OfnKYD7xeCl-9wMWm6uIc4euukl8SmZ6aC7MoCBDYyE4njQ2ceGoDPJgSQwcZmBrrglQTEAfWQsfA)

+++

### Collection Display Enhancements

* Explicit "View All" and "More Items" button
* Show statistics on Item Pages
* Suppress statistics on Collection/Community Pages
  * Numbers were misleadingly small


---

### Thank You!

Terry Brady, Suzanne Chase, Salwa Ismail, Leah Prescott

Georgetown University Library
Georgetown Law Library

![](https://www.library.georgetown.edu/sites/default/files/library-logo.png)
![](https://repository.library.georgetown.edu/themes/law-lib//images/gull_logo.jpg)
