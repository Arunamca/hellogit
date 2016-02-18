# hellogit
java

package hello;
import com.aspose.j2me.barcode.generation.BarCodeBuilder;
import com.aspose.j2me.barcode.generation.Symbology;
import com.aspose.j2me.barcode.generation.GraphicsUnit;
import javax.microedition.lcdui.CustomItem;
import javax.microedition.lcdui.Graphics;
import javax.microedition.lcdui.Image;
/**
 * Sample class for using Aspose.BarCode for J2ME
 * Shows how to create a CustomItem to paint barcodes.
 */
public class SampleBarCodeItem extends CustomItem {
    protected SampleBarCodeItem(String s) {
        super(s);
    }

    protected int getMinContentWidth() {
        return 200;
    }

    protected int getMinContentHeight() {
        return 200;
    }

    protected int getPrefContentWidth(int i) {
        return i;
    }

    protected int getPrefContentHeight(int i) {
        return i;
    }

    // Default codetext
    private String _codeText = "12345";
    // Symbology
    private long _symbology = Symbology.Code128;
    private Image _img = null;

    // Set codetext
    public void setCodeText(String code)
    {
        this._codeText = code;
    }

    // Set symbology
    public void setSymbologyType(long sym)
    {
        this._symbology = sym;
    }

    // Instance of BarCodeBuilder class
    private BarCodeBuilder barcodeBuilder;

    // Paint method for displaying the barcode image
    protected void paint(Graphics g, int w, int h) {

        // Initialize with default values, if null
        if(barcodeBuilder == null)
        {
            barcodeBuilder =  new BarCodeBuilder(_symbology,_codeText);
        }
        else
        {
            barcodeBuilder.setSymbologyType(_symbology);
            barcodeBuilder.setCodeText(_codeText);
        }

        // Set properties
        barcodeBuilder.setGraphicsUnit(GraphicsUnit.PIXEL);
        barcodeBuilder.setxDimension(2);
        barcodeBuilder.setBarHeight(50);
        barcodeBuilder.setWideNarrowRatio(2);
        barcodeBuilder.setBorderVisible(false);
        barcodeBuilder.setCodeTextVisible(true);

        // Create an image
        if(_img == null)
        {
            _img = Image.createImage(w,h);
        }

        // Get Graphics
        Graphics g1 = _img.getGraphics();

        g1.setForeColor(0xFFFFFFFF);
        g1.fillRect(0,0,w,h);

        // Render the barcode image on the display area
        barcodeBuilder.render(g1);
        g.drawImage(_img,0,0,Graphics.TOP | Graphics.LEFT);
    }

    // Call this method to draw barcode image
    public void repaintBarCode() {
        this.repaint();
    }

    // Get barcode image
    public Image getImage() {
        return this._img;
    }
}
 

Open the source view of the HelloMIDlet class and add the instance of the SampleBarCodeItem class as a member.
Add the lines of the startApp() method below to initialize the custom item.

Java

private SampleBarCodeItem bc;
public void startApp()
{
    if (midletPaused)
    {
        resumeMIDlet();
    }
    else
    {
        initialize();
        startMIDlet();

        // Initialize the custom item
        bc = new SampleBarCodeItem("Aspose-BarCode Generation ");
        this.form.append(bc);
        bc.setPreferredSize(300, 200);
    }
    midletPaused = false;
}
java

// Method to generate the barcode and render on device screen
public void generateBarcode()
{
    bc.setCodeText(txtCodetext.getString());
    bc.setSymbologyType(Symbology.Pdf417);
    bc.repaintBarCode();

}
 


 

