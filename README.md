# Script-do-yan
Boa e nova 
using UnityEngine;

public class BlocoAoPular : MonoBehaviour
{
    public GameObject blocoPrefab; // Arraste o prefab do bloco aqui
    public float alturaDoSalto = 5f;

    private Rigidbody2D rb;
    private bool estaNoChao = true;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // Detecta pulo
        if (Input.GetKeyDown(KeyCode.Space) && estaNoChao)
        {
            rb.velocity = new Vector2(rb.velocity.x, alturaDoSalto);
            CriarBloco();
        }
    }

    void CriarBloco()
    {
        Vector3 posicaoDoBloco = transform.position - new Vector3(0, 1, 0); // Um bloco abaixo do jogador
        Instantiate(blocoPrefab, posicaoDoBloco, Quaternion.identity);
    }

    void OnCollisionEnter2D(Collision2D collision)
    {
        // Detecta se tocou o chão
        if (collision.gameObject.CompareTag("Chao"))
        {
            estaNoChao = true;
        }
    }

    void OnCollisionExit2D(Collision2D collision)
    {
        if (collision.gameObject.CompareTag("Chao"))
        {
            estaNoChao = false;
        }
    }
}
