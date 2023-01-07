---
source: "blog"
title: "North Road: QGIS 3.28 improvements for working with ESRI formats and services"
image: "qgis-3-28-improvements-for-working-with-esri-formats-and-services."
date: "2022-11-24"
link: "https://north-road.com/2022/11/24/qgis-3-28-improvements-for-working-with-esri-formats-and-services/"
draft: "true"
showcase: "planet"
---

<p>The QGIS 3.28 release is an extremely exciting release for all users who work in mixed software workplaces, or who need to work alongside users of ESRI software. In this post we&#8217;ll be giving an overview of all the new tools and features introduced in 3.28 which together result in a dramatic improvement in the workflows and capabilities in working with ESRI based formats and services. Read on for the full details&#8230;!</p>
<p>Before we begin, we&#8217;d like to credit the following organisations for helping fund these developments in QGIS 3.28:</p>
<ul>
<li>Naturstyrelsen, Denmark</li>
<li>Provincie Gelderland, Netherlands</li>
<li>Uppsala Universitet, Department of Archaeology and Ancient History</li>
<li>Gemeente Amsterdam</li>
<li>Provincie Zuid-Holland, Netherlands</li>
</ul>
<h2>FileGeodatabase (GDB) related improvements</h2>
<p>The headline item here is that QGIS 3.28 introduces support for editing, managing and creating ESRI FileGeodatabases out of the box! While older QGIS releases offered some limited support for editing FileGeodatabase layers, this required the manual installation of a closed source ESRI SDK driver&#8230; which unfortunately resulted in other regressions in working with FileGeodatabases (such as poor layer loading speed and random crashes). Now, thanks to an incredible reverse engineering effort by the <a href="https://gdal.org/">GDAL</a> team, the <a href="https://gdal.org/drivers/vector/openfilegdb.html">open-source driver for FileGeodatabases</a> offers <strong>full</strong> support for editing these datasets! This means all QGIS users have out-of-the-box access to a fully functional, high-performance read AND write GDB driver, no further action or trade-offs required.</p>
<p>Operations supported by the GDAL open source driver include:</p>
<ul>
<li>Editing existing features, with full support for editing attributes and curved, 3D and measure-value geometries</li>
<li>Creating new features</li>
<li>Deleting features</li>
<li>Creating, adding and modifying attributes in an existing layer</li>
<li>Full support for reading and updating spatial indexes</li>
<li>Creating new indexes on attributes</li>
<li>&#8220;Repacking&#8221; layers, to reduce their size and improve performance</li>
<li>Creating new layers in an existing FileGeodatabase</li>
<li>Removing layers from FileGeodatabases</li>
<li>Creating completely new, empty FileGeodatabases</li>
<li>Creating and managing field domains</li>
</ul>
<p>On the QGIS side, the improvements to the GDAL driver meant that we could easily expose feature editing support for FileGeodatabase layers for all QGIS users. While this is a huge step forward, especially for users in mixed software workplaces, we weren&#8217;t happy to rest there when we  had the opportunity to further improve GDB support within QGIS!</p>
<p>So in QGIS 3.28 we also introduced the following new functionality when working with FileGeodatabases:</p>
<h3>FileGeodatabase management tools</h3>
<p>QGIS 3.28 introduces a whole range of GUI based tools for managing FileGeodatabases. To create a brand new FileGeodatabase, you can now right click on a directory from the QGIS Browser panel and select New &#8211; ESRI FileGeodatabase:</p>
<p><img decoding="async" loading="lazy" class="alignnone size-full wp-image-212448" src="https://north-road.com/wp-content/uploads/2022/11/create_geodatabase.png" alt="" width="615" height="405" srcset="https://north-road.com/wp-content/uploads/2022/11/create_geodatabase.png 615w, https://north-road.com/wp-content/uploads/2022/11/create_geodatabase-300x198.png 300w, https://north-road.com/wp-content/uploads/2022/11/create_geodatabase-230x151.png 230w, https://north-road.com/wp-content/uploads/2022/11/create_geodatabase-350x230.png 350w, https://north-road.com/wp-content/uploads/2022/11/create_geodatabase-480x316.png 480w" sizes="(max-width: 615px) 100vw, 615px" /></p>
<p>After creating your new database, a right click on its entry will show a bunch of available options for managing the database. These include options for creating new tables, running arbitrary SQL commands, and database-level operations such as compacting the database:</p>
<p><img decoding="async" loading="lazy" class="alignnone size-full wp-image-212449" src="https://north-road.com/wp-content/uploads/2022/11/new_table.png" alt="" width="528" height="349" srcset="https://north-road.com/wp-content/uploads/2022/11/new_table.png 528w, https://north-road.com/wp-content/uploads/2022/11/new_table-300x198.png 300w, https://north-road.com/wp-content/uploads/2022/11/new_table-230x152.png 230w, https://north-road.com/wp-content/uploads/2022/11/new_table-350x231.png 350w, https://north-road.com/wp-content/uploads/2022/11/new_table-480x317.png 480w" sizes="(max-width: 528px) 100vw, 528px" /></p>
<p>You&#8217;re also able to directly import existing data into a FileGeodatabase by simply dragging and dropping layers onto the database!</p>
<p>Expanding out the GDB item will show a list of layers present in the database, and present options for managing the fields in those layers. Alongside field creation, you can also remove and rename existing fields.</p>
<p><img decoding="async" loading="lazy" class="alignnone size-full wp-image-212450" src="https://north-road.com/wp-content/uploads/2022/11/create_field.png" alt="" width="589" height="218" srcset="https://north-road.com/wp-content/uploads/2022/11/create_field.png 589w, https://north-road.com/wp-content/uploads/2022/11/create_field-300x111.png 300w, https://north-road.com/wp-content/uploads/2022/11/create_field-230x85.png 230w, https://north-road.com/wp-content/uploads/2022/11/create_field-350x130.png 350w, https://north-road.com/wp-content/uploads/2022/11/create_field-480x178.png 480w" sizes="(max-width: 589px) 100vw, 589px" /></p>
<h3>Field domain handling</h3>
<p>QGIS 3.28 also introduces a range of GUI tools for working with field domains inside FileGeodatabases. (GeoPackage users also share in the love here &#8212; these same tools are all available for working with field domains inside this standard format too!) Just right click on an existing FileGeodatabase (or GeoPackage) and select the &#8220;New Field Domain&#8221; option. Depending on the database format, you&#8217;ll be presented with a list of matching field domain types:</p>
<p><img decoding="async" loading="lazy" class="alignnone size-full wp-image-212451" src="https://north-road.com/wp-content/uploads/2022/11/new_field_domain.png" alt="" width="777" height="289" srcset="https://north-road.com/wp-content/uploads/2022/11/new_field_domain.png 777w, https://north-road.com/wp-content/uploads/2022/11/new_field_domain-300x112.png 300w, https://north-road.com/wp-content/uploads/2022/11/new_field_domain-768x286.png 768w, https://north-road.com/wp-content/uploads/2022/11/new_field_domain-230x86.png 230w, https://north-road.com/wp-content/uploads/2022/11/new_field_domain-350x130.png 350w, https://north-road.com/wp-content/uploads/2022/11/new_field_domain-480x179.png 480w" sizes="(max-width: 777px) 100vw, 777px" /></p>
<p>Once again, you&#8217;ll be guided through a user-friendly dialog allowing you to create your desired field domain!</p>
<p><img decoding="async" loading="lazy" class="alignnone size-full wp-image-212452" src="https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-46-17.png" alt="" width="401" height="568" srcset="https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-46-17.png 401w, https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-46-17-212x300.png 212w, https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-46-17-230x326.png 230w, https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-46-17-350x496.png 350w" sizes="(max-width: 401px) 100vw, 401px" /></p>
<p>After field domains have been created, they can be assigned to fields in the database by right-clicking on the field name and selecting &#8220;Set Field Domain&#8221;:</p>
<p><img decoding="async" loading="lazy" class="alignnone size-full wp-image-212453" src="https://north-road.com/wp-content/uploads/2022/11/assign_domain.png" alt="" width="563" height="273" srcset="https://north-road.com/wp-content/uploads/2022/11/assign_domain.png 563w, https://north-road.com/wp-content/uploads/2022/11/assign_domain-300x145.png 300w, https://north-road.com/wp-content/uploads/2022/11/assign_domain-230x112.png 230w, https://north-road.com/wp-content/uploads/2022/11/assign_domain-350x170.png 350w, https://north-road.com/wp-content/uploads/2022/11/assign_domain-480x233.png 480w" sizes="(max-width: 563px) 100vw, 563px" /></p>
<p>Field domains can also be viewed and managed by expanding out the &#8220;Field domains&#8221; option for each database.</p>
<h3>Relationship discovery</h3>
<p>Another exciting addition in QGIS 3.28 (and the underlying GDAL 3.6 release) is support for discovering database relationships in FileGeodatabases! (Once again, GeoPackage users also benefit from this, as we&#8217;ve implemented full support for GeoPackage relationships via the &#8220;<a href="http://www.geopackage.org/spec/related-tables/">Related Tables Extension</a>&#8220;).</p>
<p>Expanding out a database containing any relationships will show a list of all discovered relationships:</p>
<p><img decoding="async" loading="lazy" class="alignnone size-full wp-image-212454" src="https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-54-51.png" alt="" width="324" height="97" srcset="https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-54-51.png 324w, https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-54-51-300x90.png 300w, https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-12-54-51-230x69.png 230w" sizes="(max-width: 324px) 100vw, 324px" /></p>
<p>(You can view the full description and details for any of these relationships by opening the QGIS Browser &#8220;Properties&#8221; panel).</p>
<p>Whenever QGIS 3.28 discovers relationships in the database, these related tables will <strong>automatically</strong> be added to your project whenever any of the layers which participate in the relationship are opened. This means that users get the full experience as designed for these databases without <strong>any</strong> manual configuration, and the relationships will &#8220;just work&#8221;!</p>
<h3>Dataset Grouping</h3>
<p>Lastly, we&#8217;ve improved the way layers from FileGeodatabases are shown in QGIS, so that layers are now grouped according to their original dataset groupings from the database structure:</p>
<p><img decoding="async" loading="lazy" class="alignnone size-full wp-image-212455" src="https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-13-15-06.png" alt="" width="329" height="215" srcset="https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-13-15-06.png 329w, https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-13-15-06-300x196.png 300w, https://north-road.com/wp-content/uploads/2022/11/Screenshot-from-2022-11-24-13-15-06-230x150.png 230w" sizes="(max-width: 329px) 100vw, 329px" /></p>
<h2>Edit ArcGIS Online / Feature Service layers</h2>
<p>While QGIS has had read-only support for viewing and working with the data in ArcGIS Online (AGOL) vector layers and ArcGIS Server &#8220;feature service&#8221; layers for many years, we&#8217;ve added support for <strong>editing</strong> these layers in QGIS 3.28. This allows you to take advantage of all of QGIS&#8217; easy to use, powerful editing tools and directly edit the content in these layers from within your QGIS projects! You can freely create new features, delete features, and modify the shape and attributes of existing features (assuming that your user account on the ArcGIS service has these edit permissions granted, of course). This is an exciting addition for anyone who has to work often with content in ArcGIS services, and would prefer to directly manipulate these layers from within QGIS instead of the limited editing tools available on the AGOL/Portal platforms themselves.</p>
<p>This new functionality will be available immediately to users upon upgrading to QGIS 3.28 &#8212; any users who have been granted edit capabilities for the layers will see that the QGIS edit tools are all enabled and ready for use without any further configuration on the QGIS client side.</p>
<h2>Filtering Feature Service layers</h2>
<p>We&#8217;ve also had the opportunity to introduce filter/query support for Feature Service layers in QGIS 3.28. This is a huge performance improvement for users who need to work with a subset of a features from a large Feature Service layer. Unfortunately, due to the nature of the Feature Service protocol, these layers can often be slow to load and navigate on a client side. By setting a SQL filter to limit the features retrieved from the service the performance can be dramatically increased, as only matching features will ever be requested from the backend server. You can use any SQL query which conforms to the subset of SQL understood by ArcGIS servers (see the Feature Service <a href="https://developers.arcgis.com/rest/services-reference/enterprise/query-feature-service-layer-.htm">documentation</a> for examples of supported SQL queries).</p>
<p>&nbsp;</p>
<p><img decoding="async" loading="lazy" class="size-full wp-image-212369 aligncenter" src="https://north-road.com/wp-content/uploads/2022/09/Peek-2022-09-16-11-11.gif" alt="" width="1233" height="797" /></p>
<h2>What&#8217;s next?</h2>
<p>While QGIS 3.28 is an extremely exciting release for any users who need to work alongside ESRI software, we aren&#8217;t content to rest here! The exciting news is that in QGIS 3.30 we&#8217;ll be introducing a GUI driven approach allowing users to create new relationships in their FileGeodatabase (and GeoPackage!) databases.</p>
<p>At North Road we&#8217;re always continuing to improve the cross-vendor experience for both ESRI and open-source users through our continued work on the QGIS desktop application and our <a href="https://north-road.com/slyr/">SLYR</a> conversion suite. If you&#8217;d like to chat to us about how we can help your workplace transition from a fully ESRI stack to a mixed or fully open-source stack, just <a href="https://north-road.com/contact/">contact us</a> to discuss your needs.</p>
<div data-animation="no-animation" data-icons-animation="no-animation" data-overlay="" data-change-size="" data-button-size="0.7" style="font-size:0.7em!important;display:none;" class="supsystic-social-sharing supsystic-social-sharing-package-flat supsystic-social-sharing-hide-on-homepage supsystic-social-sharing-spacing supsystic-social-sharing-content supsystic-social-sharing-content-align-left" data-text=""><a data-networks="[]" class="social-sharing-button sharer-flat sharer-flat-1 counter-standard without-counter twitter" target="_blank" title="Twitter" href="https://twitter.com/share?url=https%3A%2F%2Fnorth-road.com%2F2022%2F11%2F24%2Fqgis-3-28-improvements-for-working-with-esri-formats-and-services%2F&text=QGIS+3.28+improvements+for+working+with+ESRI+formats+and+services" data-main-href="https://twitter.com/share?url={url}&text={title}" data-nid="2" data-name="" data-pid="1" data-post-id="212368" data-url="https://north-road.com/wp-admin/admin-ajax.php" rel="nofollow" data-mailto=""><i class="fa-ssbs fa-ssbs-fw fa-ssbs-twitter"></i><div class="counter-wrap standard"><span class="counter">0</span></div></a><a data-networks="[]" class="social-sharing-button sharer-flat sharer-flat-1 counter-standard without-counter linkedin" target="_blank" title="Linkedin" href="https://www.linkedin.com/shareArticle?mini=true&title=QGIS+3.28+improvements+for+working+with+ESRI+formats+and+services&url=https%3A%2F%2Fnorth-road.com%2F2022%2F11%2F24%2Fqgis-3-28-improvements-for-working-with-esri-formats-and-services%2F" data-main-href="https://www.linkedin.com/shareArticle?mini=true&title={title}&url={url}" data-nid="13" data-name="" data-pid="1" data-post-id="212368" data-url="https://north-road.com/wp-admin/admin-ajax.php" rel="nofollow" data-mailto=""><i class="fa-ssbs fa-ssbs-fw fa-ssbs-linkedin"></i><div class="counter-wrap standard"><span class="counter">0</span></div></a><a data-networks="[]" class="social-sharing-button sharer-flat sharer-flat-1 counter-standard without-counter facebook" target="_blank" title="Facebook" href="http://www.facebook.com/sharer.php?u=https%3A%2F%2Fnorth-road.com%2F2022%2F11%2F24%2Fqgis-3-28-improvements-for-working-with-esri-formats-and-services%2F" data-main-href="http://www.facebook.com/sharer.php?u={url}" data-nid="1" data-name="" data-pid="1" data-post-id="212368" data-url="https://north-road.com/wp-admin/admin-ajax.php" rel="nofollow" data-mailto=""><i class="fa-ssbs fa-ssbs-fw fa-ssbs-facebook"></i><div class="counter-wrap standard"><span class="counter">0</span></div></a></div>